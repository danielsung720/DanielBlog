title: JS分割index為奇數的陣列
author: Daniel Sung Blog
tags: [JS, CODEWAR, KYU4]
categories: [學習筆記]
date: 2020-12-27 20:30:00
---
JS會開始寫一些基本的題目，因為對於ES6實在太不熟了XD
繼續泡在舒適圈會壞掉的~_~
<!-- more -->
### 題目
Write a function that returns a sequence (index begins with 1) of all the even characters from a string. If the string is smaller than two characters or longer than 100 characters, the function should return "invalid string".

For example:
```javascript
"abcdefghijklm" --> ["b", "d", "f", "h", "j", "l"]
"a"             --> "invalid string"
```

### 解答
#### My Answer
```javascript
function evenChars(string) {
  if(string.length < 2 || string.length > 100){
    return 'invalid string';
  }else{
    var res = [];
    for(var i = 1; i < string.length; i = i + 2){
      res.push(string[i]);
    }
    return res;
  }
}
```

#### Best Practices
```javascript
function evenChars(string) {
  return (string.length < 2 || string.length > 100) ? "invalid string" : 
  [...string].filter((x, i) => i % 2);
}
```

### 解析
雖然是有寫出來啦~不過看到人家的最佳解答就覺得
我還要寫個迴圈，有展開運算子和filter不是很方便的東西嗎o_o
```javascript
// 展開運算子
var str = 'abcdefghijklm';

// 輸出結果
console.log([...str]);
--> [ 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm' ]

// 這時候在配上filter，一定要配溫開水(使用箭頭函式)
console.log([...str].filter((value, index) => index % 2 === 1; ));
--> [ 'b', 'd', 'f', 'h', 'j', 'l' ]
```

## 總結
ES6真D很方便，到底IE什麼時候可以成全所有工程師阿~~~😂😂