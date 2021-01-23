title: 工作筆記-PHP Google Ad Manager API
author: Daniel Sung Blog
tags: [PHP, GOOGLE, Ad Manager]
categories: [工作筆記]
date: 2021-01-23 15:58:00
---
這禮拜真的快被這個libary搞瘋，因為網路上幾乎找不到中文的教學

英文破加上第一次閱讀google的document…真的是場硬仗
<!-- more -->
### 資源
Composer: [googleads-php-lib](.https://github.com/googleads/googleads-php-lib)
Document: [Google Ad Manager](.https://developers.google.com/ad-manager/api/start)

### 重點注意事項
#### 設定檔
首先是文件提到的adsapi_php.ini
這是最重要的，尤其是這四個參數
```ini
[AD_MANAGER]
networkCode = "INSERT_NETWORK_CODE_HERE"
applicationName = "INSERT_APPLICATION_NAME_HERE"

[OAUTH2]
jsonKeyFilePath = "INSERT_ABSOLUTE_PATH_TO_OAUTH2_JSON_KEY_FILE_HERE"
scopes = "https://www.googleapis.com/auth/dfp"
```
AD_MANAGER就是官方的API要去設定的參數
OAUTH2就有意思了，可以參考
Justin Lee Blog: [關於OAuth 2.0-以Facebook為例](.https://medium.com/@justinlee_78563/%E9%97%9C%E6%96%BCoauth-2-0-%E4%BB%A5facebook%E7%82%BA%E4%BE%8B-6f78a4a55f52)
wiki: [開放授權](.https://zh.wikipedia.org/wiki/%E5%BC%80%E6%94%BE%E6%8E%88%E6%9D%83)
doc: [document](.https://tools.ietf.org/html/rfc6749)

#### get session
其實仔細去看每一個Example，就會發現，它是需要身分驗證的
也就跟剛剛所提到的OAUTH2有關係，會發現範例中都有這樣的CODE
所以切記**adsapi_php.ini要和執行下面這段程式的檔案放在同個資料夾**
```php
$oAuth2Credential = (new OAuth2TokenBuilder())->fromFile()
    ->build();
$session = (new AdManagerSessionBuilder())->fromFile()
    ->withOAuth2Credential($oAuth2Credential)
    ->build();
```

那...如果我的adsapi_php.ini在別的資料夾怎麼辦？
別擔心，生個路徑出來給它就對了
```php
$configPath = __DIR__ . '/config/adsapi_php.ini';

$oAuth2Credential = (new OAuth2TokenBuilder())->fromFile($configPath)
    ->build();
$session = (new AdManagerSessionBuilder())->fromFile($configPath)
    ->withOAuth2Credential($oAuth2Credential)
    ->build();
```

#### service
受限於翻譯，第一次閱讀文件我還是使用了通靈
想說既然要找到我需要的資料，那就是廣告的數據
八九不離十就是找report，結果還真的被我矇到了XD
接著只要開心的把剛生出來的**session丟進ServiceFactory中的createXXXXXXService即可**
```php
$serviceFactory = new ServiceFactory();
$reportService = $serviceFactory->createReportService($session);
```

#### ohter object
接下來就是去看你所需要找的資料其他的物件怎麼去使用
好比說這次因為要找報告，有用到了**ReportQuery**
所以必須去設定你要找什麼樣的資料，像SQL那樣
這些還真的得手動去玩一玩，才知道會拉回什麼資料(汗)
到了這步驟後，建議還是去**爬一下這些物件的參數和說明**
**秘密就是裡面的註解寫得比document還清楚...**(對我來說啦😂)
```php
// 設定報告要查詢的欄位資料
$reportQuery = new ReportQuery();
$reportQuery->setDimensions(
    [
        Dimension::ORDER_ID,
    ]
);
$reportQuery->setDimensionAttributes(
    [
        DimensionAttribute::ORDER_TRAFFICKER,
    ]
);
$reportQuery->setColumns(
    [
        Column::AD_SERVER_IMPRESSIONS, 
    ]
);
```

#### 結語
其實這次最大的收穫就是學著怎麼去看懂文件和程式
以前被中文的資源寵壞了，套件裝裝範例丟丟參數放放
使用套件時完全不懂這些參數是做什麼用的，才知道自己有多廢XD
是要開始爬人家的github了...爬一次經驗值不少阿!!!