---
title: "macOS 安装jekyll"
subtitle: "安装流程和踩坑"
layout: post
author: "Lin.na"
header-style: text
catalog:    true
tags:
  - mac
  - jekyll
---

> “jekyll 是一款简单的博客系统，静态网站生成器。”  

# 概述
[jekyll](https://www.jekyll.com.cn)是一款无需数据库、评论功能或频繁的版本更新—只需关注你的内容；  
只用 Markdown、Liquid、HTML & CSS g就可以构建可部署的静态网站；  
原生支持自定义链接、分类、静态页、文章以及自定义布局。
# 环境
macOS：版本10.15.5
# 安装Homebrew
mac通过Homebrew，可以快速安装软件包。
## 科学上网  
可以通过科学上网，使用命令行安装Homebrew：


```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## 清华源
使用清华大学镜像源[下载](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)
## HomebrewCN
[国内自动安装脚本](https://gitee.com/cunkai/HomebrewCN)

# 安装ruby
Homebrew安装完成之后，使用它来安装最新版本的ruby，代码如下:

```
brew install ruby
```

输入以下命令查看ruby版本：

```
ruby --version
```

# 安装jkeyll
安装最新版本的jekyll，命令如下：

```
sudo gem install jekyll
```

因为我们将会使用Markdown语言作为标记语言，所以还需要安装kramdown，命令如下：

```
sudo gem install kramdown
```

# 运行博客
在自己的博客系统下运行以下命令，就可以在本地启动博客

```
jekyll server
```

启动后显示如下信息：

```
Server address: http://127.0.0.1:4000/
Server running... press ctrl-c to stop.
```

说明程序已经成功启动，在浏览器中输入以下地址，就可以查看自己的博客了。

```
localhost:4000
或
http://127.0.0.1:4000/
```