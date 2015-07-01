title: "recursion"
date: 2015-03-30 00:54:11
tags: php
---

## 对于递归和循环的测试代码

**递归**

```php
function reverse_r($str) {
    if(strlen($str) > 0) {
        reverse_r(substr($str, 1));
    }   
    echo substr($str, 0, 1);
    return;
}
```

**循环**
```php
function reverse_i($str) {
    for($i = 1; $i <= strlen($str); $i++) {
        echo substr($str, -$i, 1) ;
    }       
    return;
}
```

以上代码的功能是实现字符串的反转输出，两段代码是采用不同的方法，实现的同一个功能
而递归与循环最主要的不同在于：递归函数将在内存中创建几个自身的副本，而且将产生多次函数调用的开销
