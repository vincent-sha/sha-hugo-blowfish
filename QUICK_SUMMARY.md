# 问题分析总结

## 核心问题

每篇文章的 `data-oid` **不唯一**，所有从远程 API 生成的文章共享同一个值 `views_posts/_content.gotmpl`，导致：
- ✗ 阅读数同步（所有文章指向同一个 Firebase 文档）
- ✗ 点赞数同步（所有文章指向同一个 Firebase 文档）
- ✗ 无法区分各文章的统计数据

## 原因

Hugo 使用动态内容生成（`.AddPage` API），所有动态文章都来自同一个源模板 `posts/_content.gotmpl`。

Hugo 的 `.File.Path` 属性返回源文件路径，对所有动态生成的页面都是相同的值。

## 解决方案

在 `layouts/partials/extend-head.html` 中添加前端修复脚本：

当页面加载时，JavaScript 读取当前 URL 路径，动态修改 `data-oid` 和 `data-oid-likes` 属性，使每篇文章都获得唯一的标识符。

## 修复效果

- ✓ 每篇文章获得独立的 `data-oid` 值（基于其 URL 路径）
- ✓ 每篇文章独立计数阅读和点赞
- ✓ Firebase 中每篇文章有独立的文档存储数据

## 修改清单

1. **修改** `layouts/partials/extend-head.html` - 添加修复脚本
2. **创建** `layouts/partials/meta/views.html` - 优化视图计数
