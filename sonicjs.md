# SonicJS + Hugo (Blowfish) 集成指南

本文档详细说明了如何将现有的 Hugo (Blowfish 主题) 项目迁移到使用 SonicJS 作为后端 Headless CMS 的架构。

## 1. 可行性分析

*   **架构匹配**：SonicJS (基于 Cloudflare Workers 的 Headless CMS) 提供高性能 REST API，完美契合 Hugo 的构建时数据获取需求。
*   **保留主题**：通过 Hugo 的 Content Adapter 功能，可以完全保留现有的 Blowfish 主题样式和功能，无需重写前端。
*   **性能**：SonicJS 的边缘计算特性确保了极快的数据响应速度，不会拖慢 Hugo 的构建过程。

## 2. 核心实现思路

采用 **"Headless CMS + Static Site Generator"** 模式：
1.  **数据源 (SonicJS)**：管理文章、元数据和媒体资源。
2.  **构建器 (Hugo)**：构建时通过 API 拉取数据。
3.  **桥接 (Content Adapter)**：使用 Hugo v0.110+ 的 `_content.gotmpl` 功能，将 API 数据动态转换为 Hugo 页面。

## 3. 具体实施步骤

### 第一步：SonicJS 后端准备

1.  **部署**：将 SonicJS 部署到 Cloudflare Workers。
2.  **定义 Content Type**：在 SonicJS 后台创建名为 `posts` 的内容模型，字段需对应现有的 Front Matter：
    *   `title` (Text)
    *   `slug` (Text)
    *   `date` (Date)
    *   `description` (Text)
    *   `content` (Rich Text 或 Markdown)
    *   `tags` (JSON 或 Relation)
    *   `categories` (JSON 或 Relation)
    *   `featureimage` (Media/Text)

### 第二步：数据迁移 (Local Markdown -> SonicJS)

编写 Node.js 脚本将本地 `.md` 文件批量上传到 SonicJS。

**前置需求**：
```bash
npm install gray-matter axios
```

**迁移脚本示例 (`migrate.js`)**：

```javascript
const fs = require('fs');
const path = require('path');
const matter = require('gray-matter');
const axios = require('axios');

const POSTS_DIR = './content/posts';
// 替换为你的 SonicJS API 地址
const SONIC_API_URL = 'https://your-sonicjs-app.workers.dev/v1/content/posts';
const API_TOKEN = 'YOUR_SONICJS_TOKEN';

async function migrate() {
    // 过滤出 markdown 文件
    const files = fs.readdirSync(POSTS_DIR).filter(f => f.endsWith('.md') && !f.startsWith('_'));

    for (const file of files) {
        const rawContent = fs.readFileSync(path.join(POSTS_DIR, file), 'utf-8');
        const { data, content } = matter(rawContent);

        const payload = {
            title: data.title,
            slug: file.replace('.md', ''), // 或优先使用 data.slug
            date: data.date,
            description: data.description,
            content: content, // Markdown 正文
            tags: data.tags,
            categories: data.categories,
            featureimage: data.featureimage,
            status: 'published'
        };

        try {
            await axios.post(SONIC_API_URL, payload, {
                headers: { 'Authorization': `Bearer ${API_TOKEN}` }
            });
            console.log(`✅ Uploaded: ${data.title}`);
        } catch (e) {
            console.error(`❌ Failed: ${data.title}`, e.response?.data || e.message);
        }
    }
}

migrate();
```

### 第三步：Hugo 对接 (SonicJS -> Hugo)

使用 Hugo 的 Content Adapter 功能动态生成页面。

**创建文件**：`content/posts/_content.gotmpl`

**文件内容**：

```go
{{/* 1. 配置 API 地址 */}}
{{ $url := "https://your-sonicjs-app.workers.dev/v1/content/posts?limit=1000" }}

{{/* 2. 获取远程数据 (建议配置 headers 包含 token) */}}
{{/* 注意：如果 API 是公开的，可能不需要 Authorization 头 */}}
{{ $opts := dict "headers" (dict "Authorization" "Bearer YOUR_READ_TOKEN") }}
{{ $data := resources.GetRemote $url $opts | transform.Unmarshal }}

{{/* 3. 遍历数据并添加到 Hugo */}}
{{ range $data.data }} 
  {{/* 构建页面内容对象 */}}
  {{ $content := dict "mediaType" "text/markdown" "value" .content }}
  
  {{/* 构建页面参数 (Front Matter) */}}
  {{ $params := dict 
      "title" .title
      "date" (time.AsTime .date)
      "description" .description
      "tags" .tags
      "categories" .categories
      "featureimage" .featureimage
  }}

  {{/* 添加页面到 Hugo 系统 */}}
  {{ $.AddPage (dict
      "kind" "page"
      "path" .slug
      "title" .title
      "content" $content
      "params" $params
  ) }}
{{ end }}
```

## 4. 总结与建议

1.  **工作流**：迁移后，内容创作将转移到 SonicJS 后台进行。
2.  **图片资源**：建议使用 SonicJS 的媒体库托管图片，并在文章中引用远程 URL。
3.  **调试**：在本地运行 `hugo server` 时，Hugo 会实时拉取 API 数据。如果数据量巨大，可以考虑在开发环境使用本地缓存文件。
