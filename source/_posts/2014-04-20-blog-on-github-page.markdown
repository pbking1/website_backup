---
layout: post
title: "Blog on github page"
date: 2014-04-20 13:32:38 +0800
comments: true
categories: Octopress System_analyze_and_design
---

###什么是github？
{% img /images/github1.png %}

- 是一个免费的用与存放git版本控制的软件代码和内容项目。
- 每个项目都有一个主页，列出项目的源文件

###什么是github page？
- 为了使的网页简洁易懂，github就设计了pages功能
- pages功能允许用户自定义项目首页，用来代替默认的源码列表
	- 也就是说github page可以被认为是用户编写的，托管在github上的静态网页。
- github提供模板，允许站内生成网页，但也允许用户自己编写网页，然后上传。
	- 但是这种上传并不是单纯的上传，而是会经过Jekyll程序的再处理。
<!--more-->
{% img /images/git2.png %}

###什么是jekyll?
{% img /images/jekyll1.png %}

- Jekyll（发音/'dʒiːk əl/，"杰克尔")
- jekyll是一个静态站点生成器
- 它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站。
- 因此
	- 你先在本地编写符合Jekyll规范的网站源码，然后上传到github，由github生成并托管整个网站。
- 但是由于他生成的是静态网页，因此要添加评论功能或者其他的选择较少
- 并且没有数据库，所以如果网站也越大，生成时间越长。

- 目录结构
```
/jekyll_demo
　　　　|--　_config.yml
　　　　|--　_layouts
　　　　|　　　|--　default.html 
　　　　|--　_posts
　　　　|　　　|--　2012-08-25-hello-world.html
　　　　|--　index.html
``` 

- 通过简单的几条指令就可以更新博客了
```
git add .
git commit -m "first post"
git remote add origin https://github.com/username/jekyll_demo.git
git push origin gh-pages
```