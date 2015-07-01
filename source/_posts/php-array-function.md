title: "php_array_function"
date: 2015-04-12 23:25:30
tags: php
---

# 数组函数

**array_values**: 返回数组中所有的值，并给其建立数字索引

* 说明: `array array_values (array $input)`
* e.g: 

	```php
		<?php
		$array = array("size" => "XL", "color" => "gold");
		print_r(array_values($array));
		
		/*
			Array
			(
				[0] => XL
				[1] => gold
			)
		*/
	```