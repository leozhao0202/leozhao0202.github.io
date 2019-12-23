---
layout:     post                   
title:      Github+Jekyll 自建博客相关事项
subtitle:   技术控
date:       2019-12-23
author:     Leo Zhao
header-img: 
catalog: true                       # 是否归档
tags:                               #标签
    - 技术控
    - Jekyll
excerpt: 近些日子重新开始培养热血，从研究技术开始。为了督促自己，先从Github上建个个人的博客吧。
mathjax: true
---

网上有无数此类相关的文章，讲述从如何申请Github账号，到安装Github客户端，使用Git Bash，再到本机安装Jekyll，然后同步网站。

我挑了一篇 [《Github搭建个人博客（2019最新版,亲测）》](https://blog.csdn.net/xudailong_blog/article/details/78762262），大家也可以参考这篇，比较详细。

当然，万物皆无常事，凡事都有意外。这当中还是遇到很多小问题，一时间也搞得焦头烂额，约莫搞了两天才算准备停当。下面就简略讲讲，给大家一个参考：

1. #### 申请Github账号，建立仓库（Repositories）

   这个没啥难度，也没遇到问题，一步一步来就是。

   **当然，如果看到别人家的博客样式漂亮，也可以直接fork过来（fork的意思就是复制一份到你的账号下）**

2. #### 本地安装Jekyll

   如果没有fork别人的，那么就要在本地安装Jekyll，上面的参考文章里也有，但是相对复杂些，还是需要些技术背景的，简单步骤如下（详细的请见参考）

   1. 安装Ruby（**注意要安装with devkit版本的**）

      *我的系统是windows，所以下载RubyInstaller*

      ![ruby下载1](https://github.com/leozhao0202/leozhao0202.github.io/blob/master/_images/20191223_ruby%E4%B8%8B%E8%BD%BD1.PNG?raw=true)

      ![ruby下载2](https://github.com/leozhao0202/leozhao0202.github.io/blob/master/_images/20191223_ruby%E4%B8%8B%E8%BD%BD2.PNG?raw=true)

      *我的系统是64位，诸位请自选*

      ![ruby下载3](https://github.com/leozhao0202/leozhao0202.github.io/blob/master/_images/20191223_ruby%E4%B8%8B%E8%BD%BD3.PNG?raw=true)

      **注意**

      1. Ruby的安装路径一定**不能有空格**，否则一定会有错误（比如我一开始将其安装在Program Files文件夹内，结果到了安装Jekyll时，就出现了Error：makefile 263：multiple target patterns. Stop.）

      2. Ruby安装完成后，会有一个弹出的命令框，提示安装msys64，建议**直接回车**即可，时间比较长，但一定要等，安装完命令框会自己关掉

         ![20191223_installMSYS2](https://github.com/leozhao0202/leozhao0202.github.io/blob/master/_images/20191223_installMSYS2.PNG?raw=true)

   2. 安装Ruby Gems

      这个其实不需要去页面上下载，打开命令框，在命令行里输入以下命令回车即可（**确保Ruby已安装完成**）

      ```
      $ gem update --system
      ```

   3. 安装Jekyll，安装Jekyll-paginate

      上面安装完好，这个通常就不会遇到问题啦

   4. 建立Jekyll工作文件夹（比如D:\JekyllBlogs）,打开命令框，输入命令行

      ```
      cd D:\JekyllBlogs
      jekyll new myblog
      ```

      **注意** myblog为我的博客的文件夹名，以上命令完成后，D:\JekyllBlogs文件夹内会生成一个myblog的文件夹，其内有Jekyll博客网站的的页面

      ![20131223_JekyllBlog](https://github.com/leozhao0202/leozhao0202.github.io/blob/master/_images/20131223_JekyllBlog.PNG?raw=true)

3. #### 初始化博客个人信息，修改_config.yml

   ​		![20191223_config](https://github.com/leozhao0202/leozhao0202.github.io/blob/master/_images/20191223_config.PNG?raw=true)



