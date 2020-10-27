layout: post
title: PHP开发APP接口（四）
description: 通信接口数据的封装时所涉及的缓存技术以及定时任务的相关命令
category: blog
tags:
  - API
  - PHP
  - 接口
categories:
  - PHP开发APP接口
author: zhoubohan
date: 2018-09-07 09:56:00
---
### APP接口实例

#### 单例模式连接数据库
1. 单例模式的三大原则

  * 构造函数需要标记为非public(为防止外部使用new操作符创建对象)，单例类不能在其他类中实例化只能被自身实例化；<br/>
  * 拥有一个保存类的实例的静态成员变量$_instance;<br/>
  * 拥有一个访问这个实例的公共静态方法<br/>

![php-api11](/images/phpApi/php-api11.png)

---