---
layout: post
title: PHP页面静态化技术（三）
description: 通过PHP处理伪静态及通过设置服务器相关配置文件来实现静态化
category: blog
tags:
  - PHP
  - 静态化
categories:
  - PHP页面静态化技术
author: zhoubohan
date: 2016-06-01 00:00:00
---

### 通过正则表达式区分析伪静态URL地址

动态：http://example.com/index.php?type=2&cid=1 转换为静态：http://example.com/index.php/2/1.html<br/>
当访问上方动态URL时,<code>print_r($_SERVER);</code>,会发现[PATH_INFO]处显示的是 /2/1.html即我们需要的静态地址，所以我们需要使用正则匹配的方式来提取这个字符串。<br/>
![page-static-tenth](/images/pageStatic/page-static-tenth.png)

### WEB服务器rewrite配置（实现伪静态）

#### Apache下的rewrite配置

* 虚拟域名配置

 找到httpd.conf文件，开启rewrite的相关模式

![page-static-11](/images/pageStatic/page-static-11.png)

 Include conf/extra/httpd-vhosts-conf

![page-static-12](/images/pageStatic/page-static-12.png)

* http_vhosts.conf配置文件的配置信息 

![page-static-13](/images/pageStatic/page-static-13.png)

当伪静态原则开启时URL指定的物理目录或者文件确实存在时，若与规则产生冲突，返回该物理文件

* RewriteCond %{DOCUMENT_ROOT}%{REQUEST_FILENAME} !-d
* RewriteCond %{DOCUMENT_ROOT}%{REQUEST_FILENAME} !-f

所有规则配置完成后重启服务器。

#### nginx下的rewrite配置

在 /etc/nginx/conf.d 文件内添加相对应的虚拟主机的conf,并添加rewrite规则。

![page-static-14](/images/pageStatic/page-static-14.png)
