---
layout: post
title: PHP页面静态化技术（一）
description: >-
  页面静态化的实现是为了更好地利用服务器资源优化页面加载速度，提高用户体验。当用户发出请求时，服务器将对PHP语法进行分析，经过解析之后再执行。当php文件有内容输出时，该内容会先经过服务器的buffer，然后再通过TCP传递到客户端。
category: blog
tags:
  - PHP
  - 静态化
categories:
  - PHP页面静态化技术
author: zhoubohan
date: 2016-05-18 00:00:00
---
## 静态化
* 我们都知道，当用户直接访问静态页面时，服务器的响应时间会比一般访问动态页面要短。在生产过程中，如果我们能将用户要访问的动态页面先转化为静态页面即可加快用户访问页面的速度。但是需要注意的是我们静态化技术主要应用于那些页面内容不经常改动的页面。<br/>
![page-static-first](/images/pageStatic/page-static-first.png)

---

### 页面纯静态化
1. 必须将PHP的缓存开启
（在PHP配置文件php.ini中，将output_buffering = on）
2. 熟悉几个关于PHP缓冲区的相关函数<br>
<ul>
<li><code>ob_start() 打开输出控制缓冲</code></li>
<li><code>ob_get_contents() 返回输出缓冲区内容</code></li>
<li><code>ob_clean() 清空输出缓冲区</code></li>
<li><code>ob_get_clean() 得到当前缓冲区内容并删除缓冲区</code></li>
</ul>

---

### demo演示
* demo地址：[demo_page_static](https://github.com/zhoubohan/demo_page_static)<br/>
![page-static-second](/images/pageStatic/page-static-second.png)
1. 首先创建数据库连接的文件db.php
![page-static-thrid](/images/pageStatic/page-static-thrid.png)
2. 编写动态模板文件temp.php
![page-static-fifth](/images/pageStatic/page-static-fifth.png)
3. 编写index.php(判断是否生成静态文件index.shtml并生成静态文件，同时设置静态文件保存时间)
![page-static-forth](/images/pageStatic/page-static-forth.png)

---
> 在linux中可以使用定时扫描任务crontab来执行此处的index.php文件