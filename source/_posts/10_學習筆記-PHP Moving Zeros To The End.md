title: 學習筆記-PHP Moving Zeros To The End
author: Daniel Sung Blog
tags: [PHP, CODEWAR, KYU5]
categories: [學習筆記]
date: 2021-01-23 15:47:00
---
給予一個陣列，將陣列中的所有0給排序到最後回傳陣列
<!-- more -->
### 題目
Write an algorithm that takes an array and moves all of the zeros to the end, preserving the order of the other elements.
```php
// Examples
moveZeros([false,1,0,1,2,0,1,3,"a"]) // returns[false,1,1,2,1,3,"a",0,0]
```

### 解答
#### My Answer
```php
function moveZeros(array $items): array
{
    $zero = [];
    foreach($items as $k => $v) {
      if($v == '0' && $v !== false){
        $zero[] = $v;
        unset($items[$k]);
      }
    }
    return array_merge($items, $zero);
}
```

#### Best Practices
```php
function moveZeros(array $items): array {
  return array_pad(array_filter($items, function($x){return $x !== 0 and $x !== 0.0;}), count($items), 0);
}
```

### 分析
```php
// array_pad(array, length, value); 將指定的長度和值補入陣列後回傳
$arr = ["apple","banana"];
$arr = array_pad($arr, 5, "guava");

print_r($arr);
Array
(
    [0] => apple
    [1] => banana
    [2] => guava
    [3] => guava
    [4] => guava
)

// array_filter(array, callbackfunction); 使用callback過濾陣列中的值
function getGuava($v) {
  return $v == 'guava';
}

$arr = array_filter($arr, 'getGuava');

print_r($arr);
Array
(
    [2] => guava
    [3] => guava
    [4] => guava
)
```

### murmur
台北終於回暖了，開勳😊😊😊