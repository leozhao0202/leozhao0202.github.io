---
layout:     post                   
title:      Jekyll 研究笔记（一）
subtitle:   使用Github+Jekyll建站后，自然会产生将其风格化的欲望
date:       2019-12-24
categories: 技术生活
author:     Leo Zhao
catalog: true                       # 是否归档
tags:                               #标签
    - 技术控
    - Jekyll
excerpt: Jekyll是一个很有意思的，怎么说呢？工具？
mathjax: true
---

它的可塑性极强，事实上，网上有无数的Jekyll主题，无数人在其上发挥着各种奇思妙想。这种事情想想还真有意思，想必技术控都无法免俗吧。

由此，就让我们扒掉它的外衣、内衣，仔细研究研究它的身体吧，HIA HIA HIA

### 目录结构

Jekyll 的核心其实是一个<b>文本转换引擎<b>。

它的概念其实就是：你可以用你最喜欢的<b>标记语言<b>来写文章，可以是 Markdown, 也可以是 Textile, 或者就是简单的 HTML, 然后 Jekyll 就会帮你把你的文章套入一个或一系列的布局中。
<br><b>简单说，就是你的文章是裸体的，实在是有失体面，所以Jekyll在它身上穿上一套礼服，看，多冠冕堂皇，沐猴而冠，东施效颦，呃~<b>
<br><br>在整个过程中你可以设置 URL 路径，你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的<b>静态页面<b>就是你的成品了。
<br><b>就是说你可以设计礼服的样式，三点式、两点式、一点式，都随你。<b>

一个基本的 Jekyll 网站的目录结构一般是像这样的：
```
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```
来看看这些都有什么用：
