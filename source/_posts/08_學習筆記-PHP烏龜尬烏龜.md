title: 學習筆記-PHP烏龜尬烏龜
author: Daniel Sung Blog
tags: [PHP, CODEWAR, KYU6]
categories: [學習筆記]
date: 2021-01-10 21:01:00
---
計算烏龜B需要花多少時間追上烏龜A，烏龜烏龜🐢🐢🐢
<!-- more -->
### 題目
Two tortoises named A and B must run a race. A starts with an average speed of 720 feet per hour. Young B knows she runs faster than A, and furthermore has not finished her cabbage.

When she starts, at last, she can see that A has a 70 feet lead but B's speed is 850 feet per hour. How long will it take B to catch A?

More generally: given two speeds v1 (A's speed, integer > 0) and v2 (B's speed, integer > 0) and a lead g (integer > 0) how long will it take B to catch A?

The result will be an array [hour, min, sec] which is the time needed in hours, minutes and seconds (round down to the nearest second) or a string in some languages.

If v1 >= v2 then return nil, nothing, null, None or {-1, -1, -1} for C++, C, Go, Nim, Pascal,[] for Kotlin or "-1 -1 -1".
```php
// Examples
race(720, 850, 70) => [0, 32, 18] or "0 32 18"
race(80, 91, 37)   => [3, 21, 49] or "3 21 49" 
```

### 解答
#### My Answer
```php
function race($v1, $v2, $g) {
  $n = intval($g / (($v2 - $v1) / 3600));
  return $v1 >= $v2 ? NULL : [intval($n / 3600), (intval($n / 60) % 60), ($n % 60)];
}
```

#### Best Practices
```php
function race($v1, $v2, $g) {
  if($v1 >= $v2) return null;
  $h = $g / ($v2 - $v1);
  return [floor($h), (floor($h * 60) % 60), floor($h * 3600) % 60];
}
```

### 總結
這題說真的比較像是在考數學，且討論區也有人說不應該放在kyu6...是挺有同感的XD
應該要更簡單才是，程式上沒什麼好解釋...😂