title: "我的第一个php程序"
date: 2015-03-30 00:11:57
tags: php
---
## 题目要求

### 对于一个任意尺寸的矩阵，从左上角开始按顺时针方向螺旋打印9-0递减的数字，直至所有的位置都填充完成

```php
<?php
echo "####square####\n\n";
$rows = $argv[1];  # get rows
$columns = $argv[2];  # get columns
$arr = array();
$arr_base = array(9, 8, 7, 6, 5, 4, 3, 2, 1, 0);
$count = $rows * $columns;
$division = (int)($count / 10);  # get division
$modulus = $count % 10;  # get modulus
                                        
for ($i = 0; $i < $division; $i++) {
    # get complete partion
    for ($j = 9; $j >= 0; $j--) {
        array_push($arr, $j);
    }
}
                                                                                        
for ($i = 0; $i < $modulus; $i++) {
    # get left partion
    array_push($arr, $arr_base[$i]);
}
# square model
for ($i = 0; $i < $rows; $i++) {
    for ($j = 0; $j < $columns; $j++) {
        $square[$i][$j] = '-';
    }
}

# print_r($arr);
# direction
static $x = 0, $y = 0;
for ($i = 0; $i < $count; $i++) {
    if ($square[$x][$y] === '-') {
        $square[$x][$y] = $arr[$i];
        continue;
    } 
    elseif ($square[$x][$y+1] === '-' && $square[$x-1][$y+1] !== '-') {
        # go right
        $square[$x][$y+1] = $arr[$i];
        $y += 1;
        continue;
    } 
    elseif ($square[$x+1][$y] === '-') {
        # go down
        $square[$x+1][$y] = $arr[$i];
        $x += 1;
        continue;
    }
    elseif ($square[$x][$y-1] === '-') {
        # go left
        $square[$x][$y-1] = $arr[$i];
        $y -= 1;
        continue;
    }
    elseif ($square[$x-1][$y] === '-') {
        # go up
        $square[$x-1][$y] = $arr[$i];
        $x -= 1;
        continue;
    }
}
    
# print square
foreach ($square as $keyofrow => $row) {
    foreach ($row as $keyofcol => $col) {
        echo "$row[$keyofcol]";
        printf("%6s", "");
    }
    echo "\n\n";
}
```
#### <a name="fenced-code-block">运行方式</a>

```bash 
$ php [filename] [row] [column]
```
