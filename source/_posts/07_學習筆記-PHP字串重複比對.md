title: 學習筆記-PHP字串重複比對
author: Daniel Sung Blog
tags: [PHP, CODEWAR, KYU6]
categories: [學習筆記]
date: 2021-01-09 22:24:00
---
比對字串中有無重複的值，並依照指定格式輸出結果~
<!-- more -->
### 題目
The goal of this exercise is to convert a string to a new string where each character in the new string is "(" if that character appears only once in the original string, or ")" if that character appears more than once in the original string. Ignore capitalization when determining if a character is a duplicate.
```php
// Examples
"din"      =>  "((("
"recede"   =>  "()()()"
"Success"  =>  ")())())"
"(( @"     =>  "))((" 
```

### 解答
#### My Answer
```php
function duplicate_encode($word){
  $arr = array_count_values(str_split(strtoupper($word)));
  $res = '';
  for($i = 0; $i < strlen($word); $i++){
    $res .= $arr[strtoupper($word[$i])] == 1 ? '(' : ')';
  }
  return $res;
}
```

#### Best Practices
```php
function duplicate_encode($word){
  $word = str_split(strtolower($word));
  $str = "";
  foreach($word as $key){
    (count(array_keys($word,$key))>1) ? $str .= ")" : $str .= "(";
  } 
  return $str;      
}
```

### 解析
天氣很冷，不想打廢話!!!
比較看不懂的就這個用法
```php
array_keys($arr, $val);

$a = ["Horse","Cat","Dog","Dog"]; 
$b = array_keys($a, 'Dog');

print_r($b);
// 這個用法的概念就是，會將指定的值取回變成一個新的陣列
Array
(
    [0] => 2 // 因為沒有key，所以是新的index和舊的index
    [1] => 3
)
// 之後再給它Count下去就知道有沒有重複啦~
```

## 總結
台北真的很冷🥶🥶🥶