# linji.tech

林骥的个人网站。

纯静态站点，无构建步骤、无依赖。改完 HTML 直接推送到 `main` 分支，GitHub Pages 会自动发布。

## 目录结构

```
.
├── index.html          首页
├── about.html          关于（身份、时间线、数字、联系方式）
├── thinking.html       九种数据分析思维（GAP / ORS / BDI）
├── book.html           著作《数据化分析》
├── writing.html        写作与公众号
├── 404.html            自定义 404 页
├── CNAME               自定义域名（GitHub Pages 依赖此文件）
├── .nojekyll           关闭 Jekyll 处理，避免下划线文件被忽略
├── robots.txt
├── sitemap.xml
└── assets
    ├── css/style.css   全部样式（设计变量在 :root 中）
    ├── js/main.js      导航、滚动揭示、页脚年份
    └── img/favicon.svg
```

## 本地预览

```bash
cd site
python3 -m http.server 8788
# 打开 http://127.0.0.1:8788
```

直接双击 `index.html` 也能看，但用本地服务器更接近线上行为。

## 用 VS Code 编辑

仓库已内置 `.vscode/` 与 `.prettierrc`，装上编辑器后基本不用再配置：

- 打开文件夹后 VS Code 会提示安装推荐扩展（**Live Server** + **Prettier**），点安装即可
- 右键 `index.html` → **Open with Live Server** → 存盘自动刷新浏览器
- 保存时自动格式化（`editor.formatOnSave`，规则见 `.prettierrc`）
- 缩进与换行由 `.editorconfig` 统一为 2 空格 + LF

推荐扩展写在 `.vscode/extensions.json`，换机器时会被提示重装。

> 注意：Prettier 第一次格式化整份 HTML 会产生较大的 diff，这是正常的，之后每次改动就只剩你实际改的那几行。

## 部署到 GitHub Pages

### 1. 推送代码

```bash
git add -A
git commit -m "初始化个人网站"
git push -u origin main
```

### 2. 开启 Pages

仓库 → **Settings → Pages**

- **Source**：`Deploy from a branch`
- **Branch**：`main` / `/ (root)`
- **Custom domain**：填 `linji.tech`，保存

> 免费账号要求仓库为 **public** 才能使用 Pages；私有仓库需 GitHub Pro。

### 3. 配置 DNS

在域名服务商处添加以下记录（`linji.tech` 是裸域，用 A / AAAA 记录）：

| 类型    | 主机记录  | 记录值                    |
| ----- | ----- | ---------------------- |
| A     | `@`   | `185.199.108.153`      |
| A     | `@`   | `185.199.109.153`      |
| A     | `@`   | `185.199.110.153`      |
| A     | `@`   | `185.199.111.153`      |
| CNAME | `www` | `linji-tech.github.io` |

IPv6（可选）：

| 类型 | 主机记录 | 记录值 |
| --- | --- | --- |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |

### 4. 等证书、开 HTTPS

DNS 生效后（通常几分钟到几小时），回到 Settings → Pages：

- 确认提示 `DNS check successful`
- 勾选 **Enforce HTTPS**（证书签发可能需要等待一段时间）

### 5. 验证

```bash
dig +short linji.tech A        # 应返回上面的 4 个 GitHub IP
curl -I https://linji.tech     # 应返回 200
```

## 维护说明

- **改文案**：直接改对应 `.html` 文件，右侧导航、页脚在各页重复，改一处需同步其他页。
- **改配色 / 字体 / 间距**：只改 `assets/css/style.css` 顶部的 `:root` 变量即可全局生效。
- **加新页面**：复制任一页面改内容，并把导航里的链接补上（页头、页脚、`sitemap.xml` 三处）。
- **新增图片**：放进 `assets/img/`，用相对路径引用，不要用绝对路径。

## 内容来源与边界

站内事实性内容（学历、履历、著作信息、思维体系、写作数据）均来自林骥公开发布的资料：
公众号「林骥」文章、《数据化分析》一书作者简介与后记、《数据化分析 Python 实战》前言等。

站内未包含任何未经确认的私人信息。如需补充个人经历、项目或作品，请先核对事实再写入。
