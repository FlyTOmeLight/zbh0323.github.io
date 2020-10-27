layout: post
title: PHP开发APP接口（一）
description: APP通信的数据格式即及接口的方式方法了解
category: blog
tags:
  - PHP
  - 接口
  - API
categories:
  - PHP开发APP接口
author: zhoubohan
date: 2018-09-07 11:15:00
---
### 客户端服务端通信形式
![php-api1](/images/phpApi/php-api1.png)

### 通信数据格式

* XML数据
XML即扩展标记语言。可以用来标记数据定义数据类型，是一种允许用户对自己的标记语言进行定义的源语言。XML格式格式统一，跨平台和语言，非常适合通信和传输。与HTML之间的区别在于XML的节点可以自定义，而HTML不能。

![php-api2](/images/phpApi/php-api2.png)

* JSON数据
JSON数据是一种轻量级数据交换格式，具有良好的可读和快速拓展的特性。跨平台，完全独立。有数组形式和字符串形式。在生产开发环境时一般采用数组形式。

![php-api3](/images/phpApi/php-api3.png)
### APP接口的作用
<table border="1">
  <tr>
    <th>获取数据:</th>
    <td>从数据库或缓存中获取数据，然后通过接口数据返回给客户端</td>
  </tr>
  <tr>
    <th>提交数据:</th>
    <td> 通过接口提交数据给服务器，然后服务器进行入库处理或其他处理</td>
  </tr>
</table>
<br/>