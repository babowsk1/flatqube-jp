# 通貨API

{% swagger method="post" path="/{currencies}" baseUrl="https://api.flatqube.io/v1/currencies" summary="通貨データ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Request succesfull" %}
```
{
  "currency": "WEVER",
  "address": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
  "price": "0.2282687283977780064244925674",
  "priceChange": "-3.71",
  "tvl": "12209750.651450054502",
  "tvlChange": "-2.45",
  "volume24h": "555590.207631653593",
  "volumeChange24h": "22.66",
  "volume7d": "3700214.440186123499",
  "fee24h": "1660.849630640965",
  "transactionsCount24h": 768
}
```
{% endswagger-response %}
{% endswagger %}

この機能は、トークンルートアドレスから通貨データ情報を取得するために使用されます。\
\
各通貨の固有データを詳細に表示することができます。

### リクエストパラメータ

_通貨パラメータ、つまり特定の通貨アドレスが必要です_

_テストに使用するWEVERのアドレスです： 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d_

### レスポンス欄の解説

| フィールド名            | 例の値                                                                  | 説明                  |
| ----------------- | -------------------------------------------------------------------- | ------------------- |
| `currency`        | `WEVER`                                                              | 通貨シンボル              |
| `address`         | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | 希望通貨価格(米ドル)のルートアドレス |
| `priceChange`     | `-3.71`                                                              | 過去24時間の価格変動率        |
| `tvl`             | `12209750.651450054`                                                 | その通貨のTVL(米ドル)       |
| `tvlChange`       | `-2.45`                                                              | 過去24時間のTVL変化率       |
| `volume24h`       | `555590.207631653593`                                                | 過去24時間の取引量(米ドル)     |
| `volumeChange24h` | `22.66`                                                              | 過去24時間の取引量変化率       |
| `volume7d`        | `3700214.4401861234`                                                 | 過去7日間の取引量(米ドル)      |

### 例

```java
app.post('/currencies/:currencies', (req, res) => {
        console.log(`Method params: ${req.params.currencies}`)
 
        axios({
            method: 'post',
            url: `${liveApiUrl}/currencies/${req.params.currencies}`
          })
        .then(function(response){
            res.send(response.data)
        })
        .catch(function(error){
            console.error(error)
            res.send('Error')
        })
  })
```

{% swagger method="post" path="" baseUrl="https://api.flatqube.io/v1/currencies" summary="DEX 通貨 USD価格" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1": "9.892687544928"
}
```
{% endswagger-response %}
{% endswagger %}

この機能は、トークンルートアドレスで通貨価格(米ドル)を取得するために使用されます。\
\
ある通貨の換算値をUSDTで表示する場合は、どこでも使用することができます。

### リクエストパラメータ

_ボディが必要です。ポストマンテストに使用するデータです：_

```
{
  "currency_addresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"  ]
}
```

### 例

```
app.post('/currencies_usdt_prices', (req, res) => {
        console.log(`Request body data: ${req.body.currency_addresses}`)
 
        axios({
            method: 'post',
            url: `${liveApiUrl}/currencies_usdt_prices`,
            data: {
                currency_addresses: req.body.currency_addresses
              }
            })
        .then(function(response){
            res.send(response.data)
        })
        .catch(function(error){
            console.error(error)
            res.send('Error')
        })
  })
```

{% swagger method="post" path="/currencies" baseUrl="https://api.flatqube.io/v1" summary="DEX 全ての通貨情報" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

この機能は、通貨データ情報を取得するために使用されます。\
アドレスや、他にリクエストされたボディパラメータをもとに、希望通貨を取得します。\
\
全ての通貨とそのデータを一覧表で表示するために使用します。

### リクエストパラメータ

_ボディが必要です。_ポストマンテストに使用するデータです：

```
  {
  "currency_addresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"
  ],
  "limit": 0,
  "offset": 0,
  "ordering": "tvlascending",
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}
```

### レスポンス欄の解説

| フィールド名                 | 例の値                                                                  | 説明                               |
| ---------------------- | -------------------------------------------------------------------- | -------------------------------- |
| `count`                |                                                                      | 1ページあたりの通貨数                      |
| `currencies`           |                                                                      | 次のデータを含む、取得取得した全通貨一覧(以下のデータを含む)： |
| `address`              | `0:b5ff077d8ac0160559bd3c945a2a824cda12ba93ae90c2697c890656d52fc7d0` | 通貨のルートアドレス                       |
| `currency`             | `MOON`                                                               | 通貨シンボル                           |
| `fee24h`               | `2.107170214758`                                                     | 過去24時間の通貨手数料(米ドル)                |
| `priceChange`          | `-14.52`                                                             | 過去24時間の価格変動率                     |
| `transactionsCount24h` | `18`                                                                 | 過去24時間のトランザクション数                 |
| `tvl`                  | `6304.683075841390`                                                  | TVL量(米ドル)                        |
| `tvlChange`            | `-8.12`                                                              | 過去24時間のTVL変化率                    |
| `volume24h`            | `713.328162545779`                                                   | 過去24時間の取引量(米ドル)                  |
| `volume7d`             | `15925.850567579295`                                                 | 過去7日間の取引量(米ドル)                   |
| `volumeChange24h`      | `-34.83`                                                             | 過去24時間の取引量変化率                    |
| `offset`               |                                                                      | オフセット                            |
| `totalCount`           | `19`                                                                 | 取得した通貨数                          |

### 例

```
app.post('/currencies', (req, res) => {
    console.log(`Request body data: ${req.body.currency_addresses}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies`,
        data: {
            currency_addresses: req.body.currency_addresses,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            whiteListUri: req.body.whiteListUri
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```

{% swagger method="post" path="/{currencies}/prices" baseUrl="https://api.flatqube.io/v1/currencies" summary="DEX 通貨価格情報" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
[
  {
    "open": "0.997085448681",
    "high": "0.997085448681",
    "low": "0.997085448681",
    "close": "0.997085448681",
    "volume": "0",
    "openTimestamp": 1646740800000,
    "closeTimestamp": 1646744400000,
    "timestamp": 1646740800000
  },
  ...
  ]
```
{% endswagger-response %}
{% endswagger %}

この機能で、特定期間の通貨価格情報を取得します。\
\
一定期間の価格変動をグラフィックで表示します。

### リクエストパラメータ

通貨パラメータ、つまり特定の通貨アドレスが必要です。

テストに使用するDai Stablecoinのアドレスです： 0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9

ボディが必要です。ポストマンテストに使用するデータ例です：

| フィールド名      | 例の値                                                         | 説明                 |
| ----------- | ----------------------------------------------------------- | ------------------ |
| `from`      | `1646741858511` or `March 8, 2022 12:17:38.511 PM GMT time` | 期間の開始日時(UNIX形式)    |
| `timeframe` | `“H1”, “D1”`                                                | 価格データの取得期間を時間と日で設定 |
| `to`        | `1647346658513` or `March 15, 2022 12:17:38.513 PM`         | 期間の終了日時(UNIX形式)    |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### レスポンス欄の解説

| フィールド名           | 例の値              | 説明                   |
| ---------------- | ---------------- | -------------------- |
| `close`          | `0.997085448681` | 1ページあたりの通貨数          |
| `closeTimestamp` | `1646744400000`  | 取得した全通貨一覧(以下のデータを含む) |
| `high`           | `0.997085448681` | 通貨のルートアドレス           |
| `low`            | `0.997085448681` | 通貨シンボル               |
| `openTimestamp`  | `1646740800000`  | 過去24時間の通貨手数料(米ドル)    |
| `timeStamp`      | `1646740800000`  | 過去24時間の価格変化率         |
| `volume`         | `0`              | 過去24時間のトランザクション数     |

### 例

```
 app.post('/currencies/:currencies/prices', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/prices`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```

{% swagger method="post" path="/{currencies}/volume" baseUrl="https://api.flatqube.io/v1/currencies" summary="DEX通貨取引量" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "data": "524.759033605461",
    "timestamp": 1647273600000
  },
  {
    "data": "1453.839953245414",
    "timestamp": 1647277200000
  },
  {
    "data": "75.106239452670",
    "timestamp": 1647280800000
  },
  ...
]
```
{% endswagger-response %}
{% endswagger %}

この機能で、通貨取引量データ情報を取得します。

特定期間内で変化した取引量(米ドル)をグラフィックで表示します。

### レスポンス欄の解説

| フィールド名      | 例の値              | 説明                                     |
| ----------- | ---------------- | -------------------------------------- |
| `data`      | `4.471446924792` | タイムフレーム（時間足、日足など）に基づく、特定時間における特定時点の取引量 |
| `timestamp` | `1647259200000`  | 取得した取引量データの日時                          |

### リクエストパラメータ

_通貨パラメータ、つまり特定の通貨アドレスが必要です。_

テストに使用するDai Stablecoinのアドレスです： _0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9_

_ボディが必要です。ポストマンテストに使用するデータです：_

| フィールド名      | 例の値                                                         | 説明                  |
| ----------- | ----------------------------------------------------------- | ------------------- |
| `from`      | `1646741858511` or `March 8, 2022 12:17:38.511 PM GMT time` | 期間の開始日時(UNIX形式)     |
| `timeframe` | `“H1”, “D1”`                                                | 取引量データの取得期間を時間と日で設定 |
| `to`        | `1647346658513` or `March 15, 2022 12:17:38.513 PM`         | 期間の終了日時(UNIX形式)     |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### 例

```javascript
app.post('/currencies/:currencies/volume', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/volume`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```

{% swagger method="post" path="{currencies}/tvl" baseUrl="https://api.flatqube.io/v1/currencies/" summary="通貨取引量データ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
 {
    "data": "443050.967523733272",
    "timestamp": 1647302400000
  },
  {
    "data": "443050.967523733272",
    "timestamp": 1647306000000
  },
  {
    "data": "443050.967523733272",
    "timestamp": 1647309600000
  },
  ...
  ]
```
{% endswagger-response %}
{% endswagger %}

この機能で、通貨取引量データ情報を取得します。

特定期間内で変化した取引量(米ドル)をグラフィックで表示します。

### リクエストパラメータ

_通貨パラメータ、つまり特定の通貨アドレスが必要です。_

テストに使用するDai Stablecoinのアドレスです：_0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9_

_ポストマンテストに使用するデータ例です：_

| フィールド名 | 例の値                                                         | 説明              |
| ------ | ----------------------------------------------------------- | --------------- |
| `from` | `1646741858511` or `March 8, 2022 12:17:38.511 PM GMT time` | 期間の開始日時(UNIX形式) |
| `to`   | `1647346658513` or `March 15, 2022 12:17:38.513 PM`         | 期間の終了日時(UNIX形式) |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### レスポンス欄の解説

| フィールド名      | 例の値                   | 説明                                     |
| ----------- | --------------------- | -------------------------------------- |
| `data`      | `433345.034717907965` | タイムフレーム（時間足、日足など）に基づく、特定時間における特定時点のTVL |
| `timestamp` | `1647244800000`       | 取得した取引量データの日時                          |

### 例

```javascript
app.post('/currencies/:currencies/tvl', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/tvl`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```
