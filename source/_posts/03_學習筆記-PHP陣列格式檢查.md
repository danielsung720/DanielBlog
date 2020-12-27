title: 學習筆記-PHP陣列結構檢查
author: Daniel Sung Blog
tags: [PHP, CODEWAR, KYU4]
categories: [學習筆記]
date: 2020-12-27 00:27:00
---
最近又開始刷題，不過調整了一下方式
不會再像以前硬刷，不會就看解答學東西...
<!-- more -->
### 題目
Nesting Structure Comparison
Complete the function/method (depending on the language) to return true/True when its argument is an array that has the same nesting structures and same corresponding length of nested arrays as the first array.
```php
final class SameStructureAsTest extends TestCase {
  public function testDescriptionExamples() {
    $this->assertTrue(same_structure_as([1, 1, 1], [2, 2, 2])); // true
    $this->assertTrue(same_structure_as([1, [1, 1]], [2, [2, 2]])); // true
    $this->assertFalse(same_structure_as([1, [1, 1]], [[2, 2], 2])); // false
    $this->assertFalse(same_structure_as([1, [1, 1]], [[2], 2])); // false
    $this->assertTrue(same_structure_as([[[], []]], [[[], []]])); // true
    $this->assertFalse(same_structure_as([[[], []]], [[1, 1]])); //false
  }
}
```

### 解答
```php
function same_structure_as(array $a, array $b): bool {
  array_walk_recursive($a, function(&$v) { $v = 1;});
  array_walk_recursive($b, function(&$v) { $v = 1;});
  
  return serialize($a) == serialize($b);
}
```

### 解析
剛看到這題目嘗試寫了20分鐘
不外乎就是一層層的if/else以及is_array或count之類的判斷
大方向有想到用遞歸寫，但一按test記憶體就爆了XD
不過看了解答真的是讚嘆...

首先array_walk_recursive
它是一個可以自己定義function去遞歸陣列的函式
```php
$arr1 = ['apple' => 'red', 'banana' =>'yellow'];
$arr2 = [$arr1, 'guava' => 'green', 'grape' => 'purple'];

function getColor($value, $key)
{
    echo '水果:' . $key . '的顏色是' . $value . '<br>';
}

array_walk_recursive($arr2, 'getColor');

// 執行結果
水果:apple的顏色是red
水果:banana的顏色是yellow
水果:guava的顏色是green
水果:grape的顏色是purple
```

接下來是serialize
它會把傳入的參數給序列化
```php
echo serialize($arr2);

// 執行結果
a:3:{i:0;a:2:{s:5:"apple";s:3:"red";s:6:"banana";s:6:"yellow";}s:5:"guava";s:5:"green";s:5:"grape";s:6:"purple";}

// 整理
a:3:{
  i:0;
  a:2:{
    s:5:"apple";
    s:3:"red";
    s:6:"banana";
    s:6:"yellow";
    }
  s:5:"guava";
  s:5:"green";
  s:5:"grape";
  s:6:"purple";
}

// 這樣應該看得出，與原本陣列的相關性吧？
i : index
a : array
s : string
```

## 總結
```php
function same_structure_as(array $a, array $b): bool {
  // 先用array_walk_recursive把兩個陣列之中所有的val全部轉換成一樣的值
  array_walk_recursive($a, function(&$v) { $v = 1;});
  array_walk_recursive($b, function(&$v) { $v = 1;});
  
  // 接著直接序列化比對
  return serialize($a) == serialize($b);

  // 3行解決我20分鐘的煩惱...蒸蚌
}
```