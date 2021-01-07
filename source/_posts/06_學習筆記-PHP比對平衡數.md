title: 學習筆記-PHP比對平衡數
author: Daniel Sung Blog
tags: [PHP, CODEWAR, KYU7]
categories: [學習筆記]
date: 2021-01-07 22:44:00
---
把中間數兩旁的數字加總，並依照結果回傳對應值
<!-- more -->
### 題目
If the number has an odd number of digits then there is only one middle digit, e.g. 92645 has middle digit 6; otherwise, there are two middle digits , e.g. 1301 has middle digits 3 and 0

The middle digit(s) should not be considered when determining whether a number is balanced or not, e.g 413023 is a balanced number because the left sum and right sum are both 5.

Number passed is always Positive .

Return the result as String
```php
(balanced-num 7)      ==> return "Balanced"
(balanced-num 295591) ==> return "Not Balanced"
(balanced-num 959)    ==> return "Balanced"
```
大意就是說，把字串兩側的數字相加並回傳結果
如果是單數，中間數就是最中間那個（廢話
雙數的話就是中間的兩個數字（廢話again...

### 解答
#### My Answer
這題算是輕鬆解，但解的很差就是
```php
function balancedNum($num) {
  if(strlen($num) <= 2) {
    return 'Balanced';
  }
  
  $arr = str_split($num);
  $middleLen = ceil(count($arr)/2) - 1;
  $a = 0; $b = 0;
  
  for($i = 0, $j = count($arr)-1; $i < $middleLen; $i++,$j--){
    $a += $arr[$i];
    $b += $arr[$j];
  }
  
  return $a == $b ? 'Balanced' : 'Not Balanced';
}
```

#### Best Practices
```php
function balancedNum($num) {
  $take = intval((strlen($num) - 1) / 2);
  $leftSum = array_sum(str_split(substr($num, 0, $take)));
  $rightSum = array_sum(str_split(substr($num, -$take, $take)));
  return $leftSum === $rightSum ? "Balanced" : "Not Balanced";
}
```

### 解析
其實寫到一半有想到可以切陣列加總就好，但是一時半刻沒有想到文字怎麼切🤣
```php
  // 取中間數的key => *intval會無條件捨去
  $take = intval((strlen($num) - 1) / 2); 
 
  // 有趣的是，我自己寫出來的也可以替代$take
  // *ceil會無條件進位
  $middleLen = ceil(count($arr)/2) - 1;

  // 接下來就是用substr切出需要的字串
  $exp   = 556688;
  $left  = substr($num, 0, $take);      // 55, $take = intval( (6-1)/2 ) = 2
  $right = substr($num, -$take, $take); // 88
```

## 總結
這題其實算是挺簡單的，只是一時半刻還真的想不到怎麼切XD