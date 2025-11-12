# RedGarden 博客项目文档

## 📖 项目概述

这是一个基于 Hugo 构建的静态个人博客，使用 GitHub Pages 托管，Cloudflare 提供 CDN 加速。

**访问地址：** https://redgarden.dpdns.org/

## 🛠 技术栈

### 核心技术
- **Hugo** - 静态网站生成器 (v0.152.2+extended)
- **Git** - 版本控制系统
- **GitHub Pages** - 免费静态网站托管
- **GitHub Actions** - CI/CD 自动化部署
- **Cloudflare** - DNS 解析和 CDN 加速

### 主题
- **Ananke** - 响应式 Hugo 主题
- 主题地址：https://github.com/theNewDynamic/gohugo-theme-ananke

### 配置文件
- `hugo.toml` - Hugo 主配置文件
- `.github/workflows/deploy.yml` - GitHub Actions 部署配置

## 🚀 快速开始

### 本地开发

1. **克隆仓库**
   ```bash
   git clone https://github.com/Nana1mi/redgarden-blog.git
   cd redgarden-blog
   ```

2. **安装依赖**
   ```bash
   # 主题作为Git子模块，已包含在内
   git submodule update --init --recursive
   ```

3. **启动开发服务器**
   ```bash
   hugo server -D
   ```

4. **访问预览**
   - 本地：http://localhost:1313
   - 支持热重载，修改文件自动刷新

### 创建新文章

```bash
# 创建文章文件
hugo new posts/your-post-name.md

# 编辑内容后提交
git add .
git commit -m "添加新文章：文章标题"
git push origin main
```

## 📁 项目结构

```
redgarden-blog/
├── archetypes/          # 内容模板
├── assets/             # 资源文件
├── content/            # 内容目录
│   ├── _index.md       # 首页内容
│   ├── about.md        # 关于页面
│   └── posts/          # 博客文章
├── layouts/            # 布局模板
├── public/             # 生成的静态文件（自动生成）
├── static/             # 静态资源（图片、CSS、JS）
├── themes/             # Hugo 主题
│   └── ananke/         # Ananke 主题
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Actions 部署配置
├── .gitignore          # Git 忽略文件
├── .gitmodules         # Git 子模块配置
├── hugo.toml           # Hugo 主配置文件
└── claude.md           # 本文档
```

## ⚙️ 配置说明

### hugo.toml 主要配置

```toml
baseURL = 'https://redgarden.dpdns.org/'
languageCode = 'zh-cn'
title = 'RedGarden 博客'
theme = 'ananke'

description = '个人技术博客与生活随笔'

[author]
  name = '你的名字'

[menu]  # 导航菜单
[[menu.main]]
  name = '首页'
  url = '/'
  weight = 1

[taxonomies]  # 分类系统
  tag = 'tags'
  category = 'categories'
```

### 文章 Front Matter

每篇文章开头需要包含以下元数据：

```yaml
---
title: "文章标题"
date: 2025-01-02
draft: false  # false 表示发布，true 表示草稿
tags: ["标签1", "标签2"]
categories: ["分类"]
featured_image: "/images/post-image.jpg"
description: "文章描述"
---
```

## 🔄 部署流程

### 自动化部署

每次推送到 `main` 分支，GitHub Actions 会自动：

1. **Checkout** - 检出代码和子模块
2. **Setup Hugo** - 安装 Hugo 扩展版
3. **Build** - 生成静态网站
4. **Upload artifact** - 上传构建产物
5. **Deploy to GitHub Pages** - 部署到 Pages

### 手动部署

如果需要手动触发部署：

1. 进入仓库：https://github.com/Nana1mi/redgarden-blog
2. 点击 "Actions" 标签
3. 选择最新的工作流
4. 点击 "Re-run jobs" → "Re-run failed jobs"

### 部署检查清单

- [ ] 确保 `draft: false` 或删除该字段
- [ ] 图片路径正确（放在 `static/` 目录）
- [ ] Markdown 语法正确
- [ ] 推送前本地预览通过

## 🌐 域名配置

### GitHub Pages 设置

- 仓库地址：https://github.com/Nana1mi/redgarden-blog
- Pages 设置：https://github.com/Nana1mi/redgarden-blog/settings/pages
- 临时地址：https://nana1mi.github.io/redgarden-blog/
- 自定义域名：redgarden.dpdns.org

### Cloudflare DNS 配置

在 Cloudflare 中配置的 DNS 记录：

| Type | Name | Target | Proxy |
|------|------|--------|-------|
| CNAME | @ | nana1mi.github.io | Proxied |

## ✍️ 写作指南

### Markdown 基本语法

```markdown
# 一级标题
## 二级标题
### 三级标题

**粗体**
*斜体*
`行内代码`

- 列表项1
- 列表项2

[链接文字](https://example.com)
![图片](/images/pic.jpg)

> 引用内容

```代码块```
```

### 文章发布步骤

1. **创建文章**
   ```bash
   hugo new posts/my-new-post.md
   ```

2. **编辑内容**
   - 打开文件编写
   - 填写 Front Matter
   - 编写正文内容

3. **本地预览**
   ```bash
   hugo server -D
   # 访问 http://localhost:1313
   ```

4. **提交发布**
   ```bash
   git add .
   git commit -m "添加新文章：我的文章标题"
   git push origin main
   ```

5. **等待部署**（1-2分钟）

6. **验证发布**
   - 访问 https://redgarden.dpdns.org/posts/my-new-post/
   - 检查文章是否正确显示

## 🔧 自定义和扩展

### 更换主题

1. 在 https://themes.gohugo.io/ 选择主题
2. 添加主题为子模块：
   ```bash
   git submodule add https://github.com/主题作者/主题名.git themes/主题名
   ```
3. 修改 `hugo.toml`：
   ```toml
   theme = "新主题名"
   ```
4. 提交更改

### 添加评论系统

推荐方案：
- **Gitalk** - 基于 GitHub Issue
- **Utterances** - 轻量级评论组件
- **Disqus** - 国际化评论系统

### 添加访问统计

- Google Analytics
- 百度统计
- Cloudflare Analytics

## 🐛 故障排除

### 常见问题

**1. Hugo 服务器启动失败**
```bash
# 检查配置文件语法
hugo config

# 检查主题是否存在
ls themes/ananke
```

**2. 图片不显示**
- 确保图片放在 `static/` 目录
- 路径以 `/` 开头：![](/images/pic.jpg)

**3. 部署失败**
- 检查 GitHub Actions 日志
- 确保 `deploy.yml` 配置正确
- 检查分支名称是否为 `main`

**4. 域名解析问题**
- 等待 DNS 传播（最多24小时）
- 检查 Cloudflare DNS 设置
- 确认 CNAME 记录正确

### 调试命令

```bash
# 检查站点配置
hugo config

# 构建静态文件
hugo

# 检查内容
hugo --renderToMemory

# 列出所有页面
hugo list all
```

## 📚 参考资源

- [Hugo 官方文档](https://gohugo.io/documentation/)
- [Ananke 主题文档](https://github.com/theNewDynamic/gohugo-theme-ananke)
- [GitHub Pages 文档](https://docs.github.com/en/pages)
- [Markdown 语法指南](https://www.markdownguide.org/)
- [Cloudflare 文档](https://developers.cloudflare.com/)

## 📝 更新日志

### 2025-01-02
- ✅ 初始化 Hugo 博客项目
- ✅ 配置 Ananke 主题
- ✅ 设置 GitHub Actions 自动部署
- ✅ 配置 GitHub Pages
- ✅ 配置 Cloudflare DNS
- ✅ 添加示例文章
- ✅ 创建项目文档

## 💬 反馈与支持

如有疑问或建议，欢迎通过以下方式联系：

- 提交 GitHub Issue
- 发送邮件
- 在博客评论区留言

---

**构建时间：** 2025-01-02
**最后更新：** 2025-01-02
**版本：** v1.0.0
