---
title: "我的第一篇博客：Hugo 建站指南"
subtitle: "从零开始搭建个人技术博客的完整记录"
date: 2025-10-06T08:00:00+08:00
lastmod: 2025-10-07T08:00:00+08:00
draft: false
tags: ["Hugo", "建站", "新手指南", "LoveIt主题"]
categories: ["技术分享"]
author: "Damon"
description: "记录使用 Hugo 和 LoveIt 主题搭建个人博客的完整过程"
---

## 🎉 博客终于上线啦！

经过了无数次尝试和修改，我的博客终于成功运行啦！这篇文章将记录我使用 Hugo 搭建博客的整个过程和遇到的所有困难。

## 📋 技术栈选择

在开始之前，我选择了以下技术栈：

- **静态网站生成器**: Hugo v0.92.0
- **主题**: LoveIt (功能丰富，界面美观)
- **部署平台**: GitHub Pages
- **自动化部署**: GitHub Actions
- **评论系统**: Valine

## 🚀 搭建过程

### 1. 环境准备

首先需要安装 Hugo：

```bash
# macOS
brew install hugo

# Windows (使用 Chocolatey)
choco install hugo-extended

# 验证安装
hugo version
```

### 2. 创建项目

```bash
# 创建新的 Hugo 站点
hugo new site my-awesome-blog

# 进入项目目录
cd my-awesome-blog

# 初始化 Git 仓库
git init
```

### 3. 安装 LoveIt 主题

```bash
# 添加主题作为子模块
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt

# 更新子模块
git submodule update --init --recursive
```

### 4. 配置文件设置

这是最关键的一步！我的 `config.toml` 配置包含了：

- 基础站点信息
- 主题参数配置
- 多语言支持 (中文)
- 菜单配置
- 社交媒体链接

## 🎨 主要功能

### 音乐播放器

在首页集成了音乐播放器，播放坂本龙一的《Opus》：

```markdown
{{< music url="/my-awesome-blog/music/opus.mp3" name="Opus" artist="坂本龙一" cover="/my-awesome-blog/images/opus1.png" >}}
```

### 博客计时器

在关于页面添加了博客运行时间计时器，实时显示博客运行的天数、小时、分钟和秒数。

### 评论系统

集成了 Valine 评论系统，支持访客留言互动。

## 💡 遇到的问题及解决方案

### 问题1: 404 页面错误

**症状**: 标签、分类、关于等页面显示 404

**原因**: 缺少对应的页面文件

**解决方案**: 创建以下文件
- `content/posts/_index.zh-cn.md`
- `content/tags/_index.zh-cn.md`
- `content/categories/_index.zh-cn.md`
- `content/about/_index.zh-cn.md`

### 问题2: 静态资源无法加载

**症状**: 图片、音乐文件 404

**原因**: 路径配置错误

**解决方案**: 使用正确的 GitHub Pages 路径
```toml
avatarURL = "/my-awesome-blog/images/avatar.png"
```

### 问题3: 计时器功能失效

**症状**: 博客年龄计时器不显示

**原因**: shortcode 文件位置错误

**解决方案**: 创建 `layouts/shortcodes/blog-age.html`

## 🔧 部署到 GitHub Pages

### 1. GitHub Actions 配置

创建 `.github/workflows/gh-pages.yml`：

```yaml
name: GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.92.0'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

### 2. 推送到 GitHub

```bash
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/你的用户名/my-awesome-blog.git
git push -u origin main
```

## 📚 下一步计划

- [ ] 添加更多技术文章
- [ ] 集成搜索功能
- [ ] 优化 SEO
- [ ] 添加友链页面
- [ ] 集成访问统计

## 🎯 总结

搭建这个博客的过程虽然遇到了很多困难，但最终成功上线还是很有成就感的。Hugo + LoveIt 的组合确实很强大，可以快速搭建出功能丰富的个人博客。

希望这篇文章能帮助到其他想要搭建个人博客的朋友！

---

*如果你在搭建过程中遇到问题，欢迎在评论区交流讨论！*