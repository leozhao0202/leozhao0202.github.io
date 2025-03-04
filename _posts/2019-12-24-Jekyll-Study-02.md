---
layout:      post                   
title:       Jekyll 研究笔记（二）
subtitle:    本章主要讲Jekyll配置以及本地服务运行参数
date:        2019-12-24
author:      Leo Zhao 
banner_img:  assets/img/jekyll1.jpg
categories:  技术生活 
tags:        技术控
             Jekyll
---

本文讲的东西比较多，但基本上都是基础的基础。我们先从根儿上了解了解吧。

Jekyll允许你很轻松的设计你的网站，这很大程度上归功于灵活强大的配置功能。既可以在网站根目录下的 `_config.yml` 文件中配置，也可以通过<b>命令行的标记</b>来配置（<b>就是说，可以在命令框（CMD）中通过类似`jekyll serve --trace`这样的语句来配置</b>）。


### 全局配置（Global Configuration）

下表中列举了所有 Jekyll 可用的设置，和多种多样的 `选项Options` (配置文件中) 及 `标记Tags` (命令行中)。

| 设置                                                         | 选项 和 标记                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <b>Site Source</b><br>修改 Jekyll 读取文件的路径。            | `source: DIR` `-s, --source DIR`                              |
| <b>Site Destination</b><br>修改 Jekyll 写入文件的路径。<b>就是生成站点的地方。</b> | `destination: DIR` `-d, --destination DIR`                    |
| <b>Safe</b><br>禁用 [自定义插件](http://jekyllcn.com/docs/plugins/)。 | `safe: BOOL` `--safe`                                         |
| <b>Exclude</b><br>转换时排除某些文件、文件夹。<b>意思就是凡是在exclude中定义的文件夹或文件，都不会转换并在_site文件夹内生成最终页面或部件。</b> | `exclude: [DIR, FILE, ...]`                                  |
| <b>Include</b><br>转换时强制包含某些文件、文件夹。所有. 开头的文件是被默认排除的，比如`.htaccess` 是个典型的例子。<b>`htaccess`是Apache的配置文件，因此即便你定义了一个以.开头的文件并把它在Include中定义，它仍然不会被转换并生成。</b> | `include: [DIR, FILE, ...]`                                  |
| <b>Keep files</b><br/>当每次生成站点时，`destination`（默认_site文件夹）中的一切会被清理，如果你想保留某些文件，可以在此定义。例如由你的构建工具生成的文件或者资源。 | `keep_files: [DIR, FILE, ...]`                               |
| <b>Time Zone</b><br/>设置时区，这个设置作用于 `TZ` 变量， Ruby 用它来处理日期和时间。 [IANA Time Zone Database](http://en.wikipedia.org/wiki/Tz_database) 里边的都有效，比如 `America/New_York` 。默认值为操作系统的时区。 | `timezone: TIMEZONE`                                         |
| <b>Encoding</b><br/>设置文件的编码，仅 Ruby 1.9 以上可用。2.0.0　版本以后默认值为 utf-8，之前版本默认值为 nil，使用 Ruby 默认的 `ASCII-8BIT`。可以用命令 `ruby -e 'puts Encoding::list.join("\n")'` 查看 Ruby 可用的编码。 | `encoding: ENCODING`                                         |
| <b>Defaults</b><br/>设置 [YAML 头信息](http://jekyllcn.com/docs/frontmatter/) 的默认值。<b>这个以后会大讲特讲的。</b> | [详细](http://jekyllcn.com/docs/configuration/#front-matter-defaults) |

#### Destination 文件夹会在站点建立时被清理

<b>`<destination>`</b> 的内容默认<b>在站点建立时会被自动清理</b>。不是你创建的文件和文件夹会被删除。你想在 `<destination>` 保留的文件和文件夹应在 `<keep_files>` 里指定。

不要把`<destination>` 设置到重要的路径上，而应该把它作为一个暂存区域，从那里复制文件到您的web服务器。



### 编译选项（Build Command Options）

<b>这部分内容，我是没用过，因此暂时也没啥研究，有需要的同学请自便。</b>

| 设置                                                         | 选项 和 标记                           |
| ------------------------------------------------------------ | -------------------------------------- |
| <b>Regeneration</b><br>允许文件修改时自动重新生成网站。         | `-w, --watch`                          |
| <b>Configuration</b><br/>手动设置配置文件，可设置多个，且后边的配置会覆盖前边的。 | `--config FILE1[,FILE2,...]`           |
| <b>Drafts</b><br/>处理草稿                                      | `--drafts`                             |
| <b>Environment</b><br/>build 时使用特定的环境变量。             | `JEKYLL_ENV=production`                |
| <b>Future</b><br/>用将来的日期发布文章                          | `future: BOOL` `--future`               |
| <b>LSI</b><br/>为相关文章生成索引                               | `lsi: BOOL` `--lsi`                     |
| <b>Limit Posts</b><br/>限制文章的数量                           | `limit_posts: NUM` `--limit_posts NUM`  |
| <b>Force polling</b><br/>强制使用轮询。                         | `--force_polling`                      |
| <b>Verbose output</b><br/>显示详细输出。                        | `-V, --verbose`                        |
| <b>Silence Output</b><br/>在编译期间不显示的正常输出。          | `-q, --quiet`                          |
| <b>Incremental build</b><br/>启用实验特性 incremental build。Incremental build 只重建修改过的 posts 和 pages，对大型网站有显著的性能提升，但在特定情况下也会影响网站生成。 | `incremental: BOOL` `-I, --incremental` |
| <b>Liquid profiler</b><br/>生成一个Liquid概述文档来帮助你发现性能瓶颈 | `profile: BOOL` `--profile`             |



### 服务选项（Serve Command Options）

除了下边的选项， `serve` 命令还可以接收 `build` 的选项，在运行网站服务之前的编译时候使用。

<b>在本地启动jekyll服务时，可以挂在以下命令项或是上面build的命令项，已达到相应的目的。</b>

| 设置                                                         | 选项 和 标记                      |
| ------------------------------------------------------------ | --------------------------------- |
| <b>Local Server Port</b><br/>监听所给的端口                     | `port: PORT` `--port PORT`         |
| <b>Local Server Hostname</b><br/>监听所给的主机名               | `host: HOSTNAME` `--host HOSTNAME` |
| <b>Base URL</b><br/>网站的根路径                                | `baseurl: URL` `--baseurl URL`     |
| <b>Detach</b><br/>从终端命令行中分离出来                        | `detach: BOOL` `-B, --detach`      |
| <b>Skips the initial site build.</b><br/>跳过服务器启动之前，网站的初始化。 | `--skip-initial-build`            |
| <b>X.509 (SSL) Private Key</b><br/>SSL私钥                      | `--ssl-key`                       |
| <b>X.509 (SSL) Certificate</b><br/>SSL公证                      | `--ssl-cert`                      |

#### 不要在配置文件中使用 tab 制表符，

这将造成解析错误，或倒回到默认设置。请使用空格替代。



## 指定 Jekyll build 时的环境

在 编译（build）（或者生成(serve) ）参数中，你可以指定 Jekyll 的环境和参数。

例如，在你代码的条件语句中如下设置：

```YAML
{ if jekyll.environment == "production" }
   { include disqus.html }
{ endif }
```

那么，在编译你的 Jekyll 网站时，if 条件语句块中的内容不会被执行；除非你在 build 命令中还指定了一个 `production` 环境，像这样：

```YAML
JEKYLL_ENV=production jekyll build
```

<b>设置环境变量允许你只在特定环境下执行指定内容。</b>

<b>`JEKYLL_ENV` 的默认值是 `development`</b>。因此，如果你在 build 参数中省略 `JEKYLL_ENV`，那么默认为 `JEKYLL_ENV=development`。因此任何涉及条件语句 `{ if jekyll.environment == "development" }` 中的内容在 编译时都会自动显现。

而且，你的环境参数可以任意设置（不止是 `development` 或者 `production`，你还可以定义`test`或是`uat` ）。你可能想在开发环境下一些隐藏的元素，比如评论功能、百度分析。或是你想在开发环境（development environment ）增加一个“在 GitHub 中编辑”的按钮，但不显示在生产环境（production environments ）中。

在 build 命令中指定参数，当你迁移环境时，可以避免更改你配置文件中的值。

<b>这个东西在工作中是很有必要的，有时候一个项目会设置N多个环境，为了避免混淆，不要懒惰哟。</b>



## 头信息默认值

<b>这里是重点内容，请仔细阅读学习，如果没读懂，那不是我的问题，请自行再读一遍。</b>

通过使用 [YAML 头信息](http://jekyllcn.com/docs/frontmatter/)可以定义站点的页面和文章的参数。

设置一些例如布局或者自定义标题，亦或是给文章指定一个更精确的日期/时间，这都可以通过在页面或文章的头信息设置参数来实现。<b>布局，就是layout，也就是文章外面穿的那套礼服。</b>

很多时候，你会发现你在重复填写很多配置项。在每个文件里设置相同的布局，对每篇文章添加相同的分类等等。你还需要添加自定义变量，如作者名，而这对于你博客上大部分的文章来说是相同的。

Jekyll 提供了一个方法允许你在站点配置中设置这些默认值，而不是在每次创建一个新的文章或页面都需要重复此配置。要做到这一点，你可以在项目根目录下的 `_config.yml` 文件里设置 `defaults` 的值指定全站范围的默认值。

`defaults` 保存一个存储<b>`scope/value`</b>对的数组，这可以<b>为某一个特定的文件路径下的文件设置默认值</b>，或者<b>为在该路径下指定 的文件类型的文件设置默认值</b>。

假设您想给站点中的所有页面和文章设置一个默认的布局。 你要将以下语句添加到你的 `_config.yml` 文件：

```YAML
defaults:
  -
    scope:
      path: "" # 一个空的字符串代表项目中所有的文件
    values:
      layout: "default"
```

##### 完成对`_config.yml`的修改后，请重新运行命令： `jekyll serve`

主要配置文件 `_config.yml` 包含了运行时一次性读入的全局配置和变量定义，在<b>站点运行的过程中</b>并不会重新加载 `_config.yml` 文件所发生的改变，因此<b>必须手动重新运行</b>。

在这里，我们把 `values` 应用给 `scope` 路径里的所有文件。因为路径被设为空字符串，它将会应用到你项目里的<b>全部文件</b>。有时你可能不想给项目在的每个文件都设置同一个布局，例如 css 文件，为此你可以在 `scope` 下指定 `type` 的值。

```YAML
defaults:
  -
    scope:
      path: "" # 一个空的字符串代表项目中所有的文件
      type: "posts" #  在 Jekyll 2.2 里是`post`
    values:
      layout: "default"
```

现在，这只会给类型是 `posts` 的文件设置默认布局。

你可以使用的不同的类型分别是 `pages` ， `posts` ， `drafts` 或者其他你站点中的集合。当创建一个<b>`scope/value`</b>对，如果你设置了 `type`，就必须指定一个 `path`。

正如前面所提到的，您还可以给 `defaults` 设置多个<b>`scope/value`</b>对。

```YAML
defaults:
  -
    scope:
      path: ""
      type: "posts"
    values:
      layout: "my-site"
  -
    scope:
      path: "projects"
      type: "pages" # 在 Jekyll 2.2 里是`page`
    values:
      layout: "project" # 覆盖之前的默认布局
      author: "Mr. Hyde"
```

例如，以上所设置的默认值表明，所有的文章都会使用 `my-site` 布局；任何在 `projects/` 文件夹下的 html 文件会使用 `project` 布局；拥有者为 `Mr. Hyde` 的页面的布局也被设为 `project` 。

<b>通过上面的文字可以看出，posts代表的就是文章，pages代表的就是html页面。</b>

```YAML
collections:
  - my_collection:
    output: true

defaults:
  -
    scope:
      path: ""
      type: "my_collection" # 你的站点里的一个集合，复数形式
    values:
      layout: "default"
```

在上面这个例子中，在集合（Collections）中命名为 `my_collection` 的集合的布局被设为 `default` 。

##通配符模式在默认值中的应用

你还可以在设置默认值时使用通配符。 比如，为`section`文件夹内的任意一个子文件件中的 `special-page.html` 设置`specific-layout`布局。（需要至少jekyll 3.7.0版本）

```YAML
collections:
  my_collection:
    output: true

defaults:
  -
    scope:
      path: "section/*/special-page.html"
    values:
      layout: "specific-layout"
```

### 优先权

Jekyll 会应用你在 `_config.yml` 文件里 `defaults` 部分的所有配置设定。然而，你也可以通过在<b>`scope/value`</b>对之中定义一个更具体的路径来覆盖这些设定。

比如上一个例子，一开始我们设置了 `my-site` 这一默认的布局。然后，通过设置一个更具体的路径， 我们把在 `projects/` 路径下的文件的默认布局设置为 `project` 。

最后，如果你在 `_config.yml` 的 `defaults` 中设置了整个站点的默认值，那么你可以在页面或文章的文件里覆盖这些设定。你需要做的是在页面或文章的头信息里定义要覆盖的设定。例如：

```YAML
# In _config.yml
...
defaults:
  -
    scope:
      path: "projects"
      type: "pages"
    values:
      layout: "project"
      author: "Mr. Hyde"
      category: "project"
...
# In projects/foo_project.md
---
author: "John Smith"
layout: "foobar"
---
The post text goes here...
```

在站点建立时，`projects/foo_project.md` 的布局会是 `foobar`而不是`project` ，`author` 是 `John Smith`而不是 `Mr. Hyde` 。

<b>换言之就是说，`_config.yml`中定义的默认值其实优先级是最低的。</b>



## 默认配置

Jekyll 默认使用以下的配置运行，当然你也可以在配置文件或者命令行中设置这些选项。

##### 有两个 kramdown 的选项不支持

注意，由于没有被包含到 kramdown HTML 转换器中， Jekyll 当前不支持<b>`remove_block_html_tags`</b> 和 <b>`remove_span_html_tags`</b>。
<br><b>啥玩意？不支持就不支持呗。</b>

```YAML
# 目录结构
source:      .
destination: ./_site
plugins:     ./_plugins
layouts:     ./_layouts
data_source: ./_data
collections: null

# 阅读处理
safe:         false
include:      [".htaccess"]
exclude:      []
keep_files:   [".git", ".svn"]
encoding:     "utf-8"
markdown_ext: "markdown,mkdown,mkdn,mkd,md"

# 内容过滤
show_drafts: null
limit_posts: 0
future:      true
unpublished: false

# 插件
whitelist: []
gems:      []

# 转换
markdown:    kramdown
highlighter: rouge
lsi:         false
excerpt_separator: "\n\n"
incremental: false

# 服务器选项
detach:  false
port:    4000
host:    127.0.0.1
baseurl: "" # does not include hostname

# 输出
permalink:     date
paginate_path: /page:num
timezone:      null

quiet:    false
defaults: []

# Markdown 处理器
rdiscount:
  extensions: []

redcarpet:
  extensions: []

kramdown:
  auto_ids:       true
  footnote_nr:    1
  entity_output:  as_char
  toc_levels:     1..6
  smart_quotes:   lsquo,rsquo,ldquo,rdquo
  enable_coderay: false

  coderay:
    coderay_wrap:              div
    coderay_line_numbers:      inline
    coderay_line_number_start: 1
    coderay_tab_width:         4
    coderay_bold_every:        10
    coderay_css:               style
```

<b>以上一大坨，之所以叫默认设置，就是说你不去改它，世界也运行得挺美好。因此，除非你有确凿的需求，那么就保留默认即可。</b><br><br>



<b>以下三个东东，我自我感觉目前用不到，估计以后也不会用到，就不在这里赘述了，请小伙伴们自便。</b>

### [Liquid 选项](https://jekyllrb.com/docs/configuration/liquid/)
### [Markdown 选项](https://jekyllrb.com/docs/configuration/markdown/)
### [Incremental Regeneration](https://jekyllrb.com/docs/configuration/incremental-regeneration/)
