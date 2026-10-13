# MirDoch 的网页导航

一个无需构建、无需后端的静态网页仓库，使用 GitHub Pages 托管。

- 导航首页：https://mirdoch.github.io/
- 第一个门户（GPU 对比）：https://mirdoch.github.io/gpu/
- 仓库：https://github.com/MirDoch/MirDoch.github.io

## 页面结构

```text
index.html      # 中文导航页
favicon.svg     # 网站图标
gpu/index.html  # NVIDIA GPU 对比工具，数据已内嵌
.nojekyll       # 直接发布静态文件
```

GPU 页来自现有 GPUCompare 项目的 `dist/gpu-compare.html`。初次发布保留该文件的完整内容，包含 46 款显卡，数据快照为 2026-10-03。

## 发布

在仓库的 **Settings → Pages** 中，将 Source 设为 **Deploy from a branch**，选择 **main / (root)**。以后每次推送到 `main`，GitHub Pages 自动更新网站。

本仓库使用公开仓库的免费 GitHub Pages，无需绑定付费服务器或自定义域名。

## 添加新的门户

1. 在仓库下新建目录，例如 `my-tool/`，放入 `index.html` 和相关资源。
2. 在首页 `index.html` 的 `.portals` 列表中追加一个 `<li>`，将链接设为 `./my-tool/`。
3. 更新首页的入口数量并推送到 `main`。

使用相对路径，使本地预览和线上页面都能正确跳转。导航页不依赖 JavaScript；GPU 工具在浏览器中完成计算。

## 从本地 GPUCompare 更新 GPU 页

在 GPUCompare 项目目录运行：

```powershell
node tools/build.js
node tools/check.js
node tools/render-test.js
node tools/sync-portal.js
git -C portal add index.html gpu/index.html
git -C portal commit -m "Update GPU comparison page"
git -C portal push
```

`sync-portal.js` 会复制最新的单文件页面，并同步首页上的显卡数量与数据快照日期。网页数据来自 NVIDIA 官方资料，理论峰值与实际性能的差别、推算标记和来源链接保留在 GPU 页中。
