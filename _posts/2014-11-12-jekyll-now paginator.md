---
layout: post
title: jekyll-now paginator
tags:
- 技术,
- 原创,
- jekyll-now 分页
---

jekyll-now 按照jekyll的文档，设置，但是却发现不能分页，给作者发了issue，才知道原来jekyll-now暂时不支持分页  
对照了jekyll和jekyll-now的首页代码，发现主要是下列代码导致的

    for post in paginator.posts   for post in site.posts 

rewrite jekyll-now index.html

    site.posts to paginator.posts

full code:[here](https://raw.githubusercontent.com/tennc/tennc.github.io/master/index.html)


 
