title: 學習筆記-PHP Alphabet symmetry
author: Daniel Sung Blog
tags: [PHP, CODEWAR, KYU7]
categories: [學習筆記]
date: 2021-01-14 21:52:00
---
給予特定的字串陣列，並依照字序符合字母表序的方式計算後回傳答案
<!-- more -->
### 題目
Consider the word "abode". We can see that the letter a is in position 1 and b is in position 2. In the alphabet, a and b are also in positions 1 and 2. Notice also that d and e in abode occupy the positions they would occupy in the alphabet, which are positions 4 and 5.

Given an array of words, return an array of the number of letters that occupy their positions in the alphabet for each word. For example,Consider the word "abode". We can see that the letter a is in position 1 and b is in position 2. In the alphabet, a and b are also in positions 1 and 2. Notice also that d and e in abode occupy the positions they would occupy in the alphabet, which are positions 4 and 5.

Given an array of words, return an array of the number of letters that occupy their positions in the alphabet for each word. For example,
```php
// Examples
solve(["abode","ABc","xyzD"]) = [4, 3, 1]
```

### 解答
#### My Answer
```php
function solve($arr) {
  $alphabet = range('a', 'z');
  $res = [];
  
  foreach($arr as $words){
    $wordsArr = str_split($words);
    $count = 0;
    
    foreach($wordsArr as $key => $val){
      if(strtolower($val) == $alphabet[$key]){
        $count++;
      }
    }
    $res[] = $count;
  }
  
  return $res;
}
```

#### Best Practices
```php
function solve($arr) {
  $alph = range("a", "z");
  return array_map(function ($e) use ($alph) {
      return count(array_intersect_assoc($alph, str_split(strtolower($e))));
    }, $arr);
}
```

### 總結
這裡用了閉包的方式，將alph傳進array_map中
然後再用array_intersect_assoc去比對Key和Value
最後悠哉的把答案給count出來，真的是蠻厲害的👍