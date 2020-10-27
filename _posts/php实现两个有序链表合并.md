title: PHP实现两个有序链表合并
author: zhoubohan
tags:
  - PHP
  - ''
  - 链表
categories:
  - php链表相关实现
date: 2018-10-03 11:09:00
---
### 有序链表合并成一个有序链表

* 生成两个有序链表

```php
class Node
{
	var $val;
    var $next = null;
    public function __construct($val = null)
    {
    	$this->val = $val;
	}
}
//第一个链表 1,3,5,7,9
$l1 = new Node();
$l1->next = null;
$temp = $l1;
for ($i = 1;$i <=10;$i+=2) {
	$node = new Node();
    $node->val = $i;
    $temp->next = $node;
    $temp = $node;
}
//第二个链表2,4,6,8,10
$l2 = new Node();
$l2->next = null;
$temp = $l2;
for ($i = 2;$i <=10;$i+=2) {
	$node = new Node();
    $node->val = $i;
    $temp->next = $node;
    $temp = $node;
}
```

* 编写合并函数

```php
function MergeNodeList($l1,$l2)
{
	if ($l1 == null) return $l1;
    if ($l2 == null) return $l2;
    //1.遍历链表1，2比较大小，如果1节点小于2链表，则放入3链表
    $l3 = new Node();
    if ($l1->val < $l2->val) {
    	$l3 = $l1;
        $l1 = $l1->next;
    } else {
    	$l3 = $l2;
        $l2 = $l2->next;
    }//如果将上述两链表放入，则此时l2放入l3
    
    $temp = $l3;
    //2.当两个链表中有一个结束了以后，另一个链表就可以全部放进第三方链表了
    while ($l1 && $l2) {
    	if ($l1->val <= $l2->val) {
        	$temp->next = $l1;
            $l1 = $l1->next;
            $temp = $temp->next;
        } else {
        	$temp->next = $l2;
            $l2 = $l2->next;
            $temp = $temp->next;
        }
    }
     
    if ($l1 !== null) $temp->next = $l1;
    if ($l2 !== null) $temp->next = $l2;
    
    return $l3;
}
```