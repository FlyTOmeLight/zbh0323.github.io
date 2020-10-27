---
layout: post
title: PHP开发APP接口（三）
description: 通信接口数据的封装时所涉及的缓存技术以及定时任务的相关命令
category: blog
tags:
  - PHP
  - API
  - 接口
categories:
  - PHP开发APP接口
author: zhoubohan
date: 2016-07-20 00:00:00
---

### Memcache及Redis缓存
1. Memcache和Redis都是来管理数据的
2. 这些数据都是储存在内存里
3. Redis可以定期将数据备份到磁盘来实现持久化
4. Memcache只是简单的key/value缓存
5. Redis除了支持简单的k/v类型的数据以外，同时还提供list,set,hash等数据结构的储存

参考[Redis相关命令](http://www.redis.cn/documentation.html)

---

### Linux定时任务
1. crontab -e //编辑某个用户的cron任务
2. crontab -l //列出某个用户的cron服务的详细内容
3. crontab -r //删除某个用户的cron服务
4. 格式：代表 分，小时， 日， 月， 星期，"*"代表范围，"/"代表每，例如每分每秒每星期
