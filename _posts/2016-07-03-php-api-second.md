layout: post
title: PHP开发APP接口（二）
description: 通信接口数据的封装
category: blog
tags:
  - PHP
  - API
  - 接口
categories:
  - PHP开发APP接口
author: zhoubohan
date: 2016-07-03 00:00:00
---
### 封装通信接口数据的方法

* JSON方式封装接口数据方法
 PHP生成JSON数据的方法
 ![php-api4](/images/phpApi/php-api4.png)

* 通信数据标准格式
 
 
 |code|message|data|
 |---|---|---|
 |状态码|提示信息|数据|

![php-api5](/images/phpApi/php-api5.png)

* json方式如何封装数据方法
 封装类
 ![php-api6](/images/phpApi/php-api6.png)

* 如何调用
 ![php-api7](/images/phpApi/php-api7.png)

* XML方式封装接口数据方法
 PHP生成XML数据
 1. 组装字符串
 2. 调用系统函数(具体使用方法手册都有)
 <code>DomDocument</code>
 <code>XMLWriter</code>
 <code>SimpleXML</code>

 ![php-api8](/images/phpApi/php-api8.png)

* 封装成类并调用
 ![php-api9](/images/phpApi/php-api9.png)

* 综合方法进行封装
 ![php-api10](/images/phpApi/php-api10.png)

---

相关代码[DEMO]()