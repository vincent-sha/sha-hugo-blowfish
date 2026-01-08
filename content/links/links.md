---
title: "友链"
description: "分享优秀的网站"
date: 2026-01-08
showDate: false
showAuthor: false
showReadingTime: false
showTableOfContents: false
showPagination: false
showComments: true
invertPagination: false
showBreadcrumbs: true
layout: "simple"
---

{{< lead >}}
分享一些优秀的网站。
{{< /lead >}}

## 静态网站

| **名称** | **网址** | **简介** | **技术栈** |
| --- | --- | --- | --- |
| **Next.js** | [**https://nextjs.org/**](https://nextjs.org/) | 目前最流行的全栈框架，支持静态生成 (SSG) 和服务端渲染 (SSR) | React, JS/TS |
| **Hugo** | [**https://gohugo.io/**](https://gohugo.io/) | 世界上构建速度最快的生成器，适合大规模内容站点 | Go |
| **Astro** | [**https://astro.build/**](https://astro.build/) | 现代“孤岛架构”，能极大减少客户端 JS，性能极佳 | React/Vue/Svelte等 |
| **Jekyll** | [**https://jekyllrb.com/**](https://jekyllrb.com/) | GitHub Pages 官方原生支持，老牌稳定，社区资源丰富 | Ruby |
| **Hexo** | [**https://hexo.io/**](https://hexo.io/) | 中文社区极其流行，拥有大量精美博客主题，配置简单 | Node.js |
| **Docusaurus** | [**https://docusaurus.io/**](https://docusaurus.io/) | Meta出品，功能最全的文档站框架，自带搜索和多语言 | React |
| **VitePress** | [**https://vitepress.dev/**](https://vitepress.dev/) | 基于 Vite 的极速文档生成器，Vue 官方生态首选 | Vue, Vite |
| **Eleventy** | [**https://www.11ty.dev/**](https://www.11ty.dev/) | 极其简约灵活，无框架绑定，适合追求极致控制的开发者 | Node.js |
| **Gatsby** | [**https://www.gatsbyjs.com/**](https://www.gatsbyjs.com/) | 强大的 React 生态，集成 GraphQL，适合复杂数据源 | React, GraphQL |
| **MkDocs** | [**https://www.mkdocs.org/**](https://www.mkdocs.org/) | 专注于项目文档，使用 Markdown 编写，配置极其简单 | Python |
| **Docsify** | [**https://docsify.js.org/**](https://docsify.js.org/) | 无需构建步骤，运行时直接渲染 Markdown，非常轻量 | JavaScript |
| **Nuxt.js** | https://nuxt.com/ | Vue 生态中的通用框架，支持 SSG 模式 | Vue, JS/TS |
| **Zola** | [**https://www.getzola.org/**](https://www.getzola.org/) | 单个可执行文件，无依赖，速度极快 | Rust |

## 部署平台

| 平台名称 | 官网地址 | 简介 | 免费额度  |
| --- | --- | --- | --- |
| **Cloudflare Pages** | [**https://pages.cloudflare.com/**](https://pages.cloudflare.com/) | 依托 Cloudflare 顶级边缘网络，性能极佳，是目前最慷慨的平台。 | 无限流量 (Bandwidth)，无限站点数，每月 500 次构建，支持免费自定义域名。 |
| **Vercel** | [**https://vercel.com/**](https://vercel.com/) | Next.js 官方平台，开发者体验（DX）天花板，部署极速且自动化程度高。 | 每月 100GB 流量，6000 分钟构建时间，支持 Serverless 函数（有一定的运行限额）。 |
| **Netlify** | [**https://www.netlify.com/**](https://www.netlify.com/) | 静态网站托管的先驱，功能丰富，插件生态（Forms, Identity）非常成熟。 | 每月 100GB 流量，300 分钟构建时间，每月 12.5k 次函数调用，支持 1 个团队成员。 |
| **GitHub Pages** | [**https://pages.github.com/**](https://pages.github.com/) | 程序员首选，与代码仓库深度集成，完全免费且极其稳定。 | 完全免费。流量限额约 100GB/月，单个仓库大小限 1GB，站点大小限 1GB。 |
| **Firebase Hosting** | [**https://firebase.google.com/**](https://firebase.google.com/) | Google 旗下的后端云服务，适合需要集成数据库、鉴权等全栈功能的应用。 | 10GB 存储空间，360MB/天 流量，免费 SSL 及自定义域名。 |
| **Render** | [**https://render.com/**](https://render.com/) | 界面清爽，支持静态站、Web 服务及数据库的一站式托管。 | 每月 100GB 流量，无限站点，构建时长共享。 |
| **Surge.sh** | [**https://surge.sh/**](https://surge.sh/) | 为命令行而生，一个命令完成部署，适合前端开发者快速预览 Demo。 | 基本无限流量。支持自定义域名，基础功能永久免费，但自定义 SSL 证书需付费。 |
| **AWS Amplify** | [**https://aws.amazon.com/amplify/**](https://aws.amazon.com/amplify/) | 亚马逊提供的全栈开发平台，适合已有 AWS 生态或追求企业级可靠性的项目。 | 每月 15GB 流量，5GB 存储，1000 分钟构建时长（免费期通常为 12 个月）。 |

## Headless CMS

| CMS 名称 | 官网地址 | 简介 | 支持数据库 |
| --- | --- | --- | --- |
| **Strapi** | [**https://strapi.io/**](https://strapi.io/) | 全球最流行的开源 Node.js CMS，插件生态极强，适合各种规模项目。 | SQLite, PostgreSQL, MySQL, MariaDB |
| **Directus** | [**https://directus.io/**](https://directus.io/) | 实时镜像您的 SQL 数据库，将其转化为 API。不产生专有模式。 | PostgreSQL, MySQL, SQLite, Oracle, MS SQL |
| **Payload CMS** | [**https://payloadcms.com/**](https://payloadcms.com/) | 基于 Next.js，代码优先（Code-first），开发者体验极佳。 | PostgreSQL (推荐), MongoDB, SQLite |
| **Ghost** | [**https://ghost.org/**](https://ghost.org/) | 专注于出版和博客，虽然是整体式架构，但其 Headless 模式非常成熟。 | MySQL 8 (生产环境), SQLite (开发环境) |
| **KeystoneJS** | [**https://keystonejs.com/**](https://keystonejs.com/) | 基于 GraphQL 和 TypeScript 的内容平台，高度可定制。 | PostgreSQL, SQLite |
| **Sanity** | [**https://www.sanity.io/**](https://www.sanity.io/) | 注：虽非完全开源后端，但 Studio 开源。 实时结构化内容的代表。 | Content Lake (自研文档型云数据库) |
| **Decap CMS** | [**https://decapcms.org/**](https://decapcms.org/) | 原名 Netlify CMS。基于 Git 存储的 CMS，无需独立数据库。 | Git 仓库 (GitHub, GitLab, Bitbucket) |
| **PocketBase** | [**https://pocketbase.io/**](https://pocketbase.io/) | 单文件运行的轻量后端，自带鉴权、数据库和文件存储。 | SQLite (内置，含实时订阅功能) |
| **Appwrite** | [**https://appwrite.io/**](https://appwrite.io/) | 完整的 Firebase 开源替代方案，包含强大的数据库组件。 | MariaDB (底层), 支持多种后端存储适配 |