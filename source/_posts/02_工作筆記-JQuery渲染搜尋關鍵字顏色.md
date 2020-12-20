title: 工作筆記-JQuery渲染搜尋關鍵字顏色
author: Daniel Sung Blog
tags: [jQuery]
categories: [工作筆記]
date: 2020-12-20 15:49:00
---
最近在後台搜尋上遇到的需求
在後端撈取資料後顯示的指定區域文字要變成紅色
<!-- more -->
就是Google搜尋的結果顯示那樣，如下圖

### 示意圖
![google搜尋結果](/DanielBlog/images/02-1.png)


### HTML
表格範例，比方說我們今天要針對email中的文字做搜尋結果顏色顯示
為了針對表格中的指定欄位做渲染，先給它加上一個class，就叫做email

```html
    <div class="content">
        <table>
            <tr>
                <th>姓名</th>
                <th>生日</th>
                <th>電話</th>
                <th>住址</th>
            </tr>
            <tr>
                <td>王曉明</td>
                <td>1990/7/11</td>
                <td>0988123456</td>
                <td class="email">WANG_MING@gmail.com</td>
            </tr>
            <tr>
                <td>周大華</td>
                <td>1995/7/28</td>
                <td>0988765432</td>
                <td class="email">FANG_sSs@yahoo.com.tw</td>
            </tr>
        </table>
    </div>
```

![範例表格01](/DanielBlog/images/02-2.jpg)

### jQuery&&JS
```js
    // 關鍵字定義 => 直接寫入，通常會從get去拿參數(ex: email=m)，我就懶得寫QQ
    var keyword = 'm';
    // 將所有搜尋出的結果欄位變成物件
    let email = $('.email');

    // 迴圈渲染
    for(let item of email){
        // 目標字串
        let target_text = $(item).text();

        // 取得目標字串陣列(包含大小寫判斷)
        let reg = new RegExp(keyword, 'gi');
        let target_arr = target_text.match(reg);
        
        // 陣列去重
        let uni_arr = [];
        $.each(target_arr, function (index, el){
            if ($.inArray(el, uni_arr) === -1) uni_arr.push(el);
        });

        // 避開html標籤 => 先渲染小寫在選染大寫
        uni_arr = uni_arr.sort().reverse();

        if(uni_arr){
            for(let text of uni_arr){
                // 取得原始html
                let ori_html = $(item).html();
                // 渲染當前的關鍵字
                let chg_html = ori_html.replaceAll(text, text.fontcolor("red"));
                $(item).html(chg_html);
            }
        }
    }
```

<b><center>渲染結果</center></b>

![範例表格02](/DanielBlog/images/02-3.jpg)

當然，只要調整class或是jQuery，也可以隨著想針對渲染的部分作調整就是了
