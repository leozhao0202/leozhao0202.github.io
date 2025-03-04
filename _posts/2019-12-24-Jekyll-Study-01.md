---
layout:      post                   
title:       Jekyll 研究笔记（一）
subtitle:    使用Github+Jekyll建站后，自然会产生将其风格化的欲望
date:        2019-12-24
author:      Leo Zhao 
banner_img:  assets/img/jekyll1.jpg
categories:  技术生活 
tags:        技术控
             Jekyll
---

Jekyll是一个很有意思的，怎么说呢？工具？

它的可塑性极强，事实上，网上有无数的Jekyll主题，无数人在其上发挥着各种奇思妙想。这种事情想想还真有意思，想必技术控都无法免俗吧。

由此，就让我们扒掉它的外衣、内衣，仔细研究研究它的身体吧，HIA HIA HIA

### 目录结构

Jekyll 的核心其实是一个<b>文本转换引擎</b>。

它的概念其实就是：你可以用你最喜欢的<b>标记语言</b>来写文章，可以是 Markdown, 也可以是 Textile, 或者就是简单的 HTML, 然后 Jekyll 就会帮你把你的文章套入一个或一系列的布局中。
<br><b>简单说，就是你的文章是裸体的，实在是有失体面，所以 Jekyll在它身上穿上一套礼服，看，多冠冕堂皇，沐猴而冠，东施效颦，呃......</b>
<br><br>在整个过程中你可以设置 URL 路径，你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的<b>静态页面</b>就是你的成品了。
<br><b>就是说你可以设计礼服的样式，三点式、两点式、一点式，都随你。</b>

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

| 文件 / 目录                                          | 描述                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| `_config.yml`                                        | 保存配置数据。<br/>**这个文件相当重要，基本上在这里设置了与整个站点相关的全局参数。如果你在本地安装了Jekyll，修改了本文件必须要重启Jekyll服务才能生效。** |
| `_drafts`                                            | drafts（草稿）文件夹内是未发布的文章。这些文件的格式中都没有`title.MARKUP`数据。<br/>**可以通过运行`jekyll serve –draft`来预览网站以及放在草稿文件夹内的文章。** |
| `_includes`                                          | includes文件夹内通常存放着一些功能性的页面部件，比如header（页头文件）、footer（页脚文件）等。你可以直接加载这些**包含部分**（这是一个名词）到你的布局或者文章中以方便重用。<br/>**比如可以使用include将文件夹内的文件直接加载到页面内进行调用。** 例如：{% raw %}{% include footer.html %}{% endraw %} |
| `_layouts`                                           | layouts（布局）是包裹在文章外部的模板。不同的文章可以通过在`YAML头信息`中进行设置以选择不同的布局。标记({% raw %}{{ content }}{% endraw %})可以将content插入页面中。<br/>**解释一下，`YAML头信息`是写在Markdown文章页首的，用来标志文章参数的部分，比如其中会设置参数`layout:post`，意思就是本文章使用post布局。** |
| `_posts`                                             | 这里放的就是你的文章了。文件格式很重要，必须要符合:`YEAR-MONTH-DAY-title.MARKUP`或是`YEAR-MONTH-DAY-title.md`。<br/>**原本此处还有关于永久链接（Permalink）的介绍，由于我没看懂，因此就去掉了。有兴趣的同学可以自行探索。** |
| `_data`                                              | 格式化好的网站数据应放在这里。jekyll 的引擎会自动加载在该目录下所有的 yaml 文件（后缀是 .yml, .yaml, .json 或者 .csv ）。这些文件可以经由｀site.data｀访问。如果有一个members.yml文件在该目录下，你就可以通过 site.data.members 获取该文件的内容。<br/>**格式化数据，就是有一定规则的数据，如果大家用过Json的话就应该明白的。如果没用过，那么就比如有个excel表格（有表头那种）名为dept.csv，其中一列表头为HR，那我可以在页面中通过`site.data.dept.HR`来调用该列数据。** |
| `_site`                                              | 当 Jekyll 完成转换，就会将生成的页面放在这里（默认）。最好将这个目录放进你的.gitignore 文件中。<br/>**关于这个`.gitignore` 文件，文件名中有git，就说明它是Git要用到的文件，这个文件的作用就是为了通知Git哪些文件不需要添加到版本管理中。简单来说，`.gitignore` 文件中记录的文件夹或文件将不会同步到Github中去。** |
| `.jekyll-metadata`                                   | 该文件帮助 Jekyll 跟踪哪些文件从上次建立站点开始到现在没有被修改，哪些文件需要在下一次站点建立时重新生成。该文件不会被包含在生成的站点中。所以最好将它加入到你的 .gitignore 文件中去。 |
| `index.html and other HTML, Markdown, Textile files` | 如果这些文件中包含 部分，Jekyll 就会自动将它们进行转换。当然，其他的如 .html, .markdown, .md, 或者 .textile等在你的站点根目录下或者不是以上提到的目录中的文件也会被转换。 |
| `Other Files/Folders`                                  | 其他一些未被提及的目录和文件如`css`还有`images`文件夹 `favicon.ico` 等文件都将被完全拷贝到生成的site中。 |