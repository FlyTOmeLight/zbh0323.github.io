layout: post
title: MySQL数据库优化（一）
description: SQL及索引优化
category: blog
tags:
  - mysql
  - 优化
categories:
  - MySQL
  - ''
author: zhoubohan
date: 2018-09-06 18:18:00
---
#### 使用MySQL提供的sakila数据库进行演示。[MySQL演示数据库](https://dev.mysql.com/doc/index-other.html),基于MySQL版本为5.5，因为不同的MySQL版本的优化器会存在一定的差别。[演示数据库的表结构信息](https://dev.mysql.com/doc/sakila/en/sakila-installation.html)。依据步骤导入演示数据库进行操作。
---

### 如何发现有问题的SQL?
#### 使用MySQL慢查询日志对有问题的SQL进行监控；
1. 首先查看慢查询日志是否打开；
![fast-sql2](/images/fastMySQL/fast-sql2.png)
2. 发现并未打开，接着查询log中的没有索引的语句是否加入到log里；
![fast-sql3](/images/fastMySQL/fast-sql3.png)
3. 发现已经打开，如未打开则使用<code>
set global log_queries_not_using_indexes=on;
</code>
4. 接下来设置需要记录到慢查询log的SQL的超时时间；
![fast-sql4](/images/fastMySQL/fast-sql4.png)
* 对其进行设置，将其设置为1s;<code>
set global long_query_time=1;
</code>
5. 开启慢查询日志；
![fast-sql5](/images/fastMySQL/fast-sql5.png)
6. 查看慢查询日志；
![fast-sql6](/images/fastMySQL/fast-sql6.png)