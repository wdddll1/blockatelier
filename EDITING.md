# Dian坊记 · 手动编辑指南

网站地址：https://wdddll1.github.io/blockatelier/

## 在 GitHub 网页里修改

1. 打开 https://github.com/wdddll1/blockatelier ，确认分支是 main。
2. 点击要修改的文件，再点击铅笔按钮（Edit this file）。
3. 修改内容后点击 Commit changes，填写简短说明并提交到 main。
4. 在 Actions 中等待 pages build and deployment 成功，然后刷新网站。若仍显示旧内容，尝试 Ctrl+F5 或无痕窗口。

保存文件就是发布网站。较大改动可先创建分支预览确认，再合并 main。需要撤回时可以从文件 History 找回旧内容并再次提交。

## 文件与界面对应关系

| 要修改的内容 | 文件 | 搜索位置 |
| --- | --- | --- |
| 浏览器标签页标题 | index.html | `<title>` |
| 顶部站名、底部站名 | index.html | `Dian坊记` |
| 首页大标题、介绍 | index.html | `为方块世界`、`从一个小小的想法` |
| 导航名称与链接 | index.html | `<nav` |
| 公告标题和正文 | index.html | `id="journal"`、`<summary>` |
| 关于介绍 | index.html | `id="about"` |
| Mod 名称、简介、版本和链接 | content.js | 对应作品的 `name` |
| 海报与标志 | assets/ | 图片文件 |
| 页面颜色、大小、间距、手机布局 | style.css | 下面的 CSS 对照表 |
| 筛选、搜索、弹窗逻辑 | app.js | 对应函数；一般无需修改 |

index.html 和 style.css 部分内容较紧凑，建议下载仓库后用 VS Code 打开，使用“格式化文档”功能（Windows 通常是 Shift+Alt+F），再编辑；不要使用 Word 等富文本编辑器。

## 修改文案

只替换 HTML 标签中间的文字，保留标签、class、id 和链接属性。例如：

```html
<h2>小创意，大世界<span class="accent">.</span></h2>
```

可以改为：

```html
<h2>我的 Mod 作品<span class="accent">.</span></h2>
```

主标题中的 `<br>` 表示换行，`<span class="accent">` 包住的文字显示主题色。公告使用 `<details>` 包住每一条，`<summary>` 是可点击标题，`<p>` 是展开后的正文；加上 open 属性会默认展开。

## 修改 Mod

在 content.js 里，window.SITE_CONTENT.mods 数组中的每个 `{ ... }` 是一个作品。字段含义：

- id：唯一的英文编号，不要重复。
- name / english：中文名称 / 英文名称。
- category：目前使用“创造”“探索”“实用”；新增分类还需要修改 index.html 的分类按钮。
- description：简短介绍。
- poster：图片相对路径，例如 './assets/my-mod.png'。
- color：卡片点缀色，例如 '#b3d99d'。
- status：状态文字，例如 '已发布'、'开发中'。
- versions：字符串数组，例如 ['Minecraft 1.21.1', 'Fabric']；填真实支持版本。
- features：详情弹窗里的介绍列表。
- downloadUrl：真实公开的 HTTPS 下载地址；null 时禁用。
- developmentUrl：真实开发页地址；null 时禁用。

例如（地址仅示意，替换为自己的真实地址）：

```js
downloadUrl: 'https://github.com/你的用户名/你的Mod仓库/releases/download/v1.0.0/你的Mod.jar',
developmentUrl: 'https://github.com/你的用户名/你的Mod仓库',
```

推荐先把 JAR 上传到自己公开仓库的 Releases，再从 Assets 复制下载链接。不要把下载地址填成仓库里的 JAR 文件查看页。

字段之间使用英文逗号，文本保留引号。单引号字符串中要输入单引号时用 \' 转义，或者改用双引号包围。增加作品时复制完整对象并用逗号分隔，同时更新 index.html 里“全部作品”的数量。

正式替换内容后，也要更新预览说明、卡片底部“版本资料待补充”及详情中的演示提示。后两项在 app.js 中；仅改 status 不会自动移除这些提示。

## 上传图片

进入 assets 目录，点击 Add file → Upload files 上传 PNG、JPG、WebP 或 SVG。在 content.js 中修改 poster 路径。文件名建议只用英文、数字和短横线，注意大小写。当前海报比例为 4:3，推荐 1200×900，过大的图片先压缩。

更换左上角标志时可以替换 assets/mark.svg，也可以上传新图片并修改 index.html 中的 img src；浏览器图标由 link rel="icon" 单独指定。

## 调整 UI 样式

style.css 中的 :root 是全站颜色设置：

```css
--bg: #131614;       /* 整页底色 */
--panel: #1a1e1b;    /* 卡片和弹窗底色 */
--text: #eff1e9;     /* 主要文字 */
--muted: #959e94;    /* 次要文字 */
--line: #30372f;     /* 边框与分割线 */
--green: #c2ef80;    /* 主题强调色 */
```

其他常用位置：

| CSS 选择器 | 控制的界面 |
| --- | --- |
| .header、.brand | 顶部导航与站名 |
| .wrap | 内容最大宽度、两侧留白 |
| .hero h1 | 首页标题大小与行高 |
| .button、.primary | 按钮形状与主题色 |
| .mod-grid | 作品卡片列数和间距 |
| .mod-card、.card-body | 卡片边框、底色与内部留白 |
| .poster-button img | 海报比例与裁剪方式 |
| .journal、.entries | 公告区域 |
| .about、.footer | 关于区域与页脚 |
| dialog、.detail-body | 弹窗 |
| @media(max-width:650px) | 手机界面覆盖样式 |
| @keyframes arrive | 淡入动画 |

font-size 调字体大小，padding 调内部留白，margin 调外部间距，border-radius 调圆角，gap 调排列间距。单位通常是 px；颜色用 #十六进制。

同一选择器可能出现多次，手机部分会覆盖前面的样式。修改后同时检查电脑和手机。网站支持“减少动态效果”系统偏好。

## 检查

发布后用无痕窗口查看：站名和文案、分类与搜索、海报弹窗、公告、手机排版、下载链接及外部开发页。网站公开访问无需 GitHub 登录；在 GitHub 编辑代码则需要登录你的账号。
