# Dian坊记 · Minecraft Mod 发布页

个人 Mod 作品站的第一版布局演示，静态 HTML / CSS / JavaScript，无需安装依赖。当前作品、版本和概念海报均为演示，尚未提供真实 JAR。

公开网站：https://wdddll1.github.io/blockatelier/

## 本地查看

直接打开 index.html，或运行 `python -m http.server 4173` 后访问 http://localhost:4173 。

## 更新网站

GitHub Pages 使用 main 分支根目录。提交修改后会自动部署；发布状态可在仓库 Actions 和 Settings → Pages 查看。

- `content.js`：作品名称、简介、分类、海报、版本、下载链接和开发页链接。
- `index.html`：站名、首页文字、公告、作者介绍和链接。
- `style.css`：颜色、排版、动画及手机布局。
- `assets/`：本地图片、概念海报和标志。

将 downloadUrl 填为真实的公开 HTTPS JAR 下载链接，例如自己的 GitHub Releases 附件链接；将 developmentUrl 填为作品开发页。空链接保持禁用，不会生成假下载。替换演示资料时，也请修改“概念演示”、预览说明与相关版本提示。

## 功能

作品分类、搜索与空结果提示、海报放大、详情弹窗、键盘 Escape 关闭、焦点返回、公告展开收起、锚点跳转、手机适配及减少动态效果支持。所有资源随网站托管，未使用外部字体或脚本。

## 访问

网站自身无登录要求。GitHub Pages 的公网可达性取决于访问者网络，可在 VPN 连接后用未登录的无痕窗口访问验证。

本站非 Minecraft / Mojang / Microsoft 官方网站。

详细修改说明：[手动编辑指南](EDITING.md)。
