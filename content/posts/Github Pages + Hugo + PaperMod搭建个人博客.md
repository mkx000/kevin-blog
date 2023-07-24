---
title: "Github Pages + Hugo + PaperMod搭建个人博客"
date: 2023-07-08T16:46:59+08:00
draft: false
# cover:
#     image: "imgs/kuafu.jpg"
#     alt: "Hugo logo"
#     caption: "Hugo logo"
#     hidden: false
summary: "This post provides an overview of Hugo (PaperMod theme) and details the steps I took in setting up this website."
tags: ["Hugo", "PaperMod", "Blog", "Website"]
---

### 测试环境

WSL2 + VSCode

### 安装必要的软件包

```bash
# 安装hugo
sudo apt install hugo
```

### 创建网站

```bash
# 创建网站, 替换your-website-name为自己想要的名字
hugo new site your-website-name -f yml
```

### 配置网站

[You can learn more and see more configuration settings that work with the PaperMod theme in the documentation.](https://adityatelange.github.io/hugo-PaperMod/)

### 本地运行网站

```bash
# 进入网站目录
cd your-website-name
# 下载主题
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
# 运行网站
hugo server -D
```
