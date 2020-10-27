layout: post
title: PHP页面静态化技术（二）
description: 我们将实现PHP的局部动态化，也就是说静态化的页面存在“动态”过程，结合全部静态化技术+Ajax技术实现局部动态化，局部更新页面。
category: blog
tags:
  - PHP
  - 静态化
categories:
  - PHP页面静态化技术
author: zhoubohan
date: 2016-05-21 00:00:00
---
### 局部动态化即伪静态的实现

 为实现局部静态化，需要结合Ajax技术。当访问主页index.php时,根据静态页面的缓存时效,判断是否生成index.shtml静态页面,当静态页面返回后静态页面中的js发起Ajax请求,获取服务器中的数据,进行动态更新。那么这里就需要一个服务器文件接口,响应Ajax请求。<br/>
 其他文件与完全静态化的文件结构相同，仅增加服务器接口的相关文件。<br/>
![page-static-sixth](/images/pageStatic/page-static-sixth.png)

---

### demo实现
demo地址： [demo_page_static](https://github.com/zhoubohan/demo_page_static2)
1. 增加接口文件api.php<br>
![page-static-seventh](/images/pageStatic/page-static-seventh.png)
2. 创建Ajax所在的js文件
![page-static-eighth](/images/pageStatic/page-static-eighth.png)
3. 修改模板文件引入js实现局部动态
![page-static-nineth](/images/pageStatic/page-static-nineth.png)