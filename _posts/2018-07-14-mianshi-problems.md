layout: post
title: 面试总结(链家)
description: 每天都是新开始，不积跬步无以至千里。
category: blog
date: 2018-09-06 18:21:30
---
### 1.判断IPV4的IP是否合法(两种方法255.255.255.255)
```php
1. 自行写函数

function checkIp(string $ip)
{
   $arr = explode('.', $ip);
   if (count($arr) ! = 4) {
       return false;
   } else {
       foreach ($arr as $v) {
           if (($v < '0' || $v > '255')) {
               return false;
           }
       }
   }

   return true;
}
```
```php
2. 使用php5.2.0之后的内置函数,判断是否为合法IP

if (filter_var($ip, FILTER_VALIDATE_IP)) {
    //it's valid
}else {
   //it's not valid 
}
```

```php
3.判断是否为合法IPV4 IP

if (filter_var($ip, FILTER_VALIDATE_IP, FILTER_FLAG_IPV4)) {
    //it's valid
}else {
   //it's not valid 
}
```
```php
4.判断是否是合法的公共IPv4地址，192.168.1.1这类的私有IP地址将会排除在外

if (filter_var($ip, FILTER_VALIDATE_IP, FILTER_FLAG_IPV4| FILTER_FLAG_NO_PRIV_RANGE)) {
    //it's valid
}else {
   //it's not valid 
}
```

```php
5.判断是否是合法的IPv6地址

if (filter_var($ip, FILTER_VALIDATE_IP, FILTER_FLAG_NO_RES_RANGE)) {
    //it's valid
}else {
   //it's not valid 
}
```

```php
6.判断是否是合法公共的IPv6地址或者IPV4地址

if (filter_var($ip, FILTER_VALIDATE_IP, FILTER_FLAG_NO_RES_RANGE|FILTER_FLAG_NO_PRIV_RANGE)) {
    //it's valid
}else {
   //it's not valid 
}
```

### 2. MySQL索引问题（联合索引或者单独索引是否生效）

- 如果条件里有or,则即使其中有条件带索引也不会使用
- like,REGEXP查询以%开头（以%结尾时是生效的）
- 查询字符串字段没有加引号则索引不会生效
- mysql使用全表扫描要比使用索引快
- where语句里有不等号<b>!=</b>，无法使用索引（负向索引）(not in失效，in生效)
- where查询条件里索引字段带有函数类似<b>DAY(column)</b>，则无法使用索引
- <b>is null,is not null</b>无法使用索引
- 
- 在联合查询里（join）里，MySQL只有在主键和外键数据类型完全相同时才能使用索引
- MySQL组合索引的生效原则（最左前缀原则，从前至后生效）

<br>

|sql语句条件&emsp;&emsp;|是否生效&emsp;&emsp;|备注&emsp;&emsp;|
|---|---|---|
|where a=3 and b=2 and c=5|生效|中间没有断点，完全发挥作用|
|where a=3 and c=5|a生效,c不生效|b作为断点|
|where b=3 and c=4|b,c均不生效|a作为断点，这种写法联合索引完全发挥作用|
|where b=4 and c=3 and a=2|生效|三者全部用上了之后与顺序无关|
|where a=3 and b>7 and c=2|a,b生效,c不生效|b作为范围值作为断点，则c不生效但是b本身生效
|where a>4 and b=5 and c=5|a生效,b,c不生效|同上|
|where a=3 order by b|a生效,b在结果排序中也是用上了索引的|
|where a=3 order by c|a生效,c不生效|没有b产生了断点|
|where b=3 order by a|都没有生效|


<br>


### 3. 一个大数组，如何打印出出现次数最多的元素

```php
function countValues($file_dir='')
{
   $str = file_get_contents($file_dir);
    preg_match_all('/\w+\/', $str, $matches);
    foreach ($matches[0] as $w) {
        $arr[$w]++; 
    }
    arsort($arr);
    return $arr;
}
```
> 即通过正则比较，一个个比较，如果相同则计数器++，如果不相等则跳过，依次比较

### 4.PHP反射机制实现自动依赖注入

```php
<?php

/*
*依赖注入，控制反转
*/

class Ioc 
{
    //获得类的实例对象
    public static function getInstance($className)
    {
        $paramArr = self::getMethodParams($className);
        return (new ReflectionClass($className))->newInstanceArgs($paramArr);
    }

    /** 
     * 执行类的方法
     */
    public static function make($className, $methodsName, $params = [])
    {
        //获取类的实例
        $instance = self::getInstance($className);
        //获取该方法需要依赖注入的参数
        $paramArr = self::getMethodParams($className, $methodsName);

        return $instance->{$methodsName}(...array_merge($paramArr, $params));
    }

    /**
     * 获得类的方法参数，只获得有类型的参数
     */
    protected static function getMethodParams($className, $methodsName = '__construct')
    {
        //通过反射获得该类
        $class = new ReflectionClass($className);
        $paramArr = []; //记录参数和参数类型

        //判断该类是否有构造类
        if ($class->hasMethod($methodsName)) {
            //获得构造函数
            $contruct = $class->getMethod($methodsName);
            //判断构造函数是否有参数
            $params = $contruct->getParameters();

            if (count($params) > 0) {
                //判断参数类型
                foreach ($params as $key => $param) {
                    if ($paramClass = $param->getClass()) {
                        //获得参数类型名称
                        $paramClassName = $paramClass->getName();

                        //获取参数类型
                        $args = self::getMethodParams($paramClassName);
                        $paramArr[] = (new ReflectionClass($paramClass->getName()))->newInstanceArgs($args);
                    }
                }
            }
        }

        return $paramArr;
    }
}
```

> 使用php内置反射类代码创建了一个容器类，使用该类实现对其他类的依赖注入功能，上面的依赖注入方法分为两种，一种是方法的依赖注入<code>make</code>，一种是构造函数的依赖注入<code>getMethodParams</code>,接下来用其他类进行测试

```php
class A
{
    protected $cObj;

    /** 
     * 用于测试多级依赖注入B依赖A，A依赖C
     */
    
    public function __construct(C $c)
    {
        $this->cObj = $c;

    }

    public function aa()
    {
        echo 'this is A-test';
    }

    public function aac()
    {
        $this->cObj->cc();
    }
}
```

```php
class B
{
    protected $aObj;

    /** 
     * 用于测试多级依赖注入B依赖A，A依赖C
     */
    
    public function __construct(A $a)
    {
        $this->aObj = $a;

    }

    public function bb(C $c, $b)
    {
        $c->cc();
        echo "\r\n";
        echo 'params:'.$b;
    }

    public function bbb()
    {
        $this->aObj->aac();
    }
}
```

```php
class C
{
    public function cc()
    {
        echo 'this is C->cc';
    }
}
```

```php
$bObj = Ioc::getInstance('B');
$bObj->bbb();

var_dump($bObj);
```

> 测试结果为

![mianshi-1](/images/mianshi/mianshi-1.png)

> 即依赖注入成功，aObj和cObj成功。