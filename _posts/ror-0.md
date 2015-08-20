title: RoR中对于Time类扩展
date: 2015-08-20 16:50:41
tags: RoR
---
今天是七夕，又被虐单身。。。
8.12塘沽爆炸了，悼念一下。。今天看新闻塘沽那边的海河区域死了好多鱼。。

唉， 开始正题：

今天突然对MySQL中的BETWEEN...AND的边界问题拿不准了，所以去查看了一下文档，以下定义附上

* ``expr BETWEEN min AND max``

If ``expr`` is greater than or equal to ``min`` and ``expr`` is less than or equal to ``max``, BETWEEN returns 1, otherwise it returns 0.
This is equivalent to the expression (min <= expr AND expr <= max) if all the arguments are of the same type. 

```mysql
mysql> SELECT 2 BETWEEN 1 AND 3, 2 BETWEEN 3 and 1;
        -> 1, 0
mysql> SELECT 1 BETWEEN 2 AND 3;
        -> 0
mysql> SELECT 'b' BETWEEN 'a' AND 'c';
        -> 1
mysql> SELECT 2 BETWEEN 2 AND '3';
        -> 1
mysql> SELECT 2 BETWEEN 2 AND 'x-3';
        -> 0
```
For best results when using BETWEEN with date or time values, use CAST() to explicitly convert the values to the desired data type. 
Examples: If you compare a DATETIME to two DATE values, convert the DATE values to DATETIME values. If you use a string constant 
such as '2001-1-1' in a comparison to a DATE, cast the string to a DATE.

得到的结论就是左右边界均是闭合的

---

今天在编写Rails中的时间段搜索时，在文档中看到一个强大得写法
``User.where({ created_at: (Time.now.midnight - 1.day)..Time.now.midnight })``

直接在项目中用到，如下：
```rails
      count_a = IntegralOrder.where({
                                      created_at: Time.now.midnight..(Time.now.midnight.tomorrow - 1),
   shop_id: @shop_id,
                                                                                                                              open_id: @user_openid,
                                                                                                                                                                      item_id: integral_order.item_id
                                                                                                                                                                                                          }).count
