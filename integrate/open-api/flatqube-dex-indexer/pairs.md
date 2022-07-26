# ペアAPI

{% swagger method="post" path="/pairs" baseUrl="https://api.flatqube.io/v1" summary="ペアデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
 ...
"counter": "BRIDGE",
        "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
        "fee": "0.3000"
      },
      "tvl": "8955040.156573434959",
      "tvlChange": "3.26",
      "leftLocked": "22564291945792668",
      "leftPrice": "0.2323725625631798673951181204",
...
}
```
{% endswagger-response %}
{% endswagger %}

この機能は、全てのペアデータを取得するために使用されます。\
\
各通貨の固有データを詳細に表示することができます。

### リクエストパラメータ

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名              | 例の値                                                                        | 説明            |
| ------------------- | -------------------------------------------------------------------------- | ------------- |
| `currencyAddress`   | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`       | 左ペアの通貨アドレス    |
| `currencyAddresses` | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`       | アドレス一覧        |
| `limit`             | `0`                                                                        | 取得すべきペア数      |
| `offset`            | `0`                                                                        |               |
| `ordering`          | `tvlascending`                                                             | ペアのTVL(昇順・降順) |
| `tvlAmountGe`       | `8955040.156573434959`                                                     | 最高TVL量        |
| `tvlAmountLe`       | `8955043.156573434959`                                                     | 最低TVL量        |
| `whiteListUri`      | `https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json` | ホワイトリストへのパス   |

```
{
  "currencyAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
  "currencyAddresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"
  ],
  "limit": 0,
  "offset": 0,
  "ordering": "tvlascending",
  "tvlAmountGe": "8955040.156573434959",
  "tvlAmountLe": "8955043.156573434959",
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}
```

### レスポンス欄の解説

| フィールド名            | 例の値                                                                  | 説明                          |
| ----------------- | -------------------------------------------------------------------- | --------------------------- |
| `count`           | `0`                                                                  | 1ページに表示されるペア数               |
| `offset`          | `0`                                                                  |                             |
| `pairs`           |                                                                      | 次のデータを含むペア一覧：               |
| `fee24h`          | `184.89949`                                                          | 過去24時間の手数料総額(米ドル)           |
| `fee7d`           | `1531.12412`                                                         | <p>過去7日間の手数料総額<br>(米ドル)</p> |
| `feeAllTime`      | `5886.2023`                                                          | EVER手数料総額(米ドル)              |
| `leftLocked`      | `22564291945792668`                                                  | 左ペア(トークン)のTVL(米ドル)          |
| `leftPrice`       | `0.234234123`                                                        | 左ペアの価格(米ドル)                 |
| `meta`            |                                                                      | 次のデータを含むオブジェクト：             |
| `base`            | `WEVER`                                                              | 左トークンの名称(例：WEVER)           |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | 左トークンのルートアドレス               |
| `counter`         | `BRIDGE`                                                             | 右トークンの名称(例：BRIDGE)          |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | 右トークンのルートアドレス               |
| `fee`             | `0.300`                                                              | 左/右トークンの取引手数料               |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | 左右ペアのプールアドレス                |
| `rightLocked`     | `565424319668420`                                                    | 右ペア(トークン)のTVL(米ドル)          |
| `rightPrice`      | `9.306709686682`                                                     | 右ペアの価格(米ドル)                 |
| `tvl`             | `8955040.156573434959`                                               | ペアプールのTVL                   |
| `tvlChange`       | `3.26`                                                               | 過去24時間におけるプール内TVL変化率        |
| `volume24h`       | `61614.202233211332`                                                 | 過去24時間におけるペアの取引量(米ドル)       |
| `volume7d`        | `563110.817462570605`                                                | 過去7日間におけるペアの取引量(米ドル)        |
| `volumeChange24h` | `85.03`                                                              | 過去24時間の取引量変化率               |
| `totalCount`      | `1`                                                                  | 検索パラメータを満たすペアの総数            |

### 例

```
app.post('/pairs', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs`,
        data: {
            currencyAddress: req.body.currencyAddress,
            currency_addresses: req.body.currency_addresses,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            tvlAmountGe: req.body.tvlAmountGe,
            tvlAmountLe: req.body.tvlAmountLe,
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

{% swagger method="post" path="/pairs/address/{address}" baseUrl="https://api.flatqube.io/v1" summary="Dexペアデータ情報" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "meta": {
    "base": "WEVER",
    "baseAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
    "counterAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
    "counter": "BRIDGE",
    "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
    "fee": "0.3000"
  },
  "tvl": "11991318.532110678860",
  "tvlChange": "1.58",
  "leftLocked": "25793313867480582",
  "leftPrice": "0.2324501340486766469128429809",
  "rightLocked": "644828780315691",
  "rightPrice": "9.298063996337",
  "volume24h": "71793.071260381244",
  "volumeChange24h": "-40.15",
  "volume7d": "1568911.947379165588",
  "fee24h": "215.553088264148",
  "fee7d": "4697.356377562167",
  "feeAllTime": "18787.266129440217"
}
```
{% endswagger-response %}
{% endswagger %}

この機能は、流動性プールアドレスからペアデータ情報を取得するためのものです。

特定のプールにあるペアの詳細を表示するために使用します。

### リクエストパラメータ

アドレスパラメータ、つまり、特定のペアのプールアドレスが必要です。\
_テストに使用するWEVER/BRIDGEのプールアドレスです：`0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06`_

### レスポンス欄の解説

| フィールド名            | 例の値                                                                  | 説明                    |
| ----------------- | -------------------------------------------------------------------- | --------------------- |
| `meta`            | _\`\`_                                                               | 次のデータを含むオブジェクト：       |
| `base`            | _`WEVER`_                                                            | 左トークンの名称(例：WEVER)     |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | 左トークンのルートアドレス         |
| `counter`         | `BRIDGE`                                                             | 右トークンの名称(例：BRIDGE)    |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | 右トークンのルートアドレス         |
| `fee`             | `0.3000`                                                             | 左/右トークンの取引手数料         |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | 左右ペアのプールアドレス          |
| `tvl`             | `11992480.952892429456`                                              | ペアプールのTVL             |
| `tvlChange`       | `1.22`                                                               | 過去24時間におけるプール内TVL変化率  |
| `leftLocked`      | `25795814233390122`                                                  | 左ペア(トークン)のTVL(米ドル)    |
| `leftPrice`       | `0.2324501340486766469128429809`                                     | 左ペアの価格(米ドル)           |
| `rightLocked`     | `644766509092723`                                                    | 右ペア(トークン)のTVL(米ドル)    |
| `rightPrice`      | `9.299863426349`                                                     | 右ペアの価格(米ドル)           |
| `volume24h`       | `68293.598448021590`                                                 | 過去24時間におけるペアの取引量(米ドル) |
| `volumeChange24h` | `-44.98`                                                             | 過去24時間の取引量変化率         |
| `volume7d`        | `1549070.057378500757`                                               | 過去7日間におけるペアの取引量(米ドル)  |
| `fee24h`          | `205.053510628491`                                                   | 過去24時間の手数料総額(米ドル)     |
| `fee7d`           | `4637.831319664494`                                                  | 過去7日間の手数料総額(米ドル)      |
| `feeAllTime`      | `18789.418763913485`                                                 | EVER手数料総額(米ドル)        |

### 例

```
 app.post('/pairs/address/:address', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/address/${req.params.address}`
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

{% swagger method="post" path="/pairs/cross_pairs" baseUrl="https://api.flatqube.io/v1" summary="Dexクロスペアデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "meta": {
    "base": "WEVER",
    "baseAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
    "counterAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
    "counter": "BRIDGE",
    "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
    "fee": "0.3000"
  },
  "tvl": "11992480.952892429456",
  "tvlChange": "1.22",
  "leftLocked": "25795814233390122",
  "leftPrice": "0.2324501340486766469128429809",
  "rightLocked": "644766509092723",
  "rightPrice": "9.299863426349",
  "volume24h": "68293.598448021590",
  "volumeChange24h": "-44.98",
  "volume7d": "1549070.057378500757",
  "fee24h": "205.053510628491",
  "fee7d": "4637.831319664494",
  "feeAllTime": "18789.418763913485"
}
```
{% endswagger-response %}
{% endswagger %}

この機能は、全てのクロスペアデータを取得するために必要です。

これは、ある通貨に関する詳細と、それがもう一方の通貨にどのように影響するか、またはその逆が必要な場合にどこでも使用できます。

### リクエストパラメータ

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名                | 例の値                                                                  | 説明                                      |
| --------------------- | -------------------------------------------------------------------- | --------------------------------------- |
| `fromCurrencyAddress` | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | クロスペアを取得する通貨アドレス                        |
| `toCurrencyAddresses` | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | 通貨アドレスパラメータから、その通貨を含むペアであるかどうかを確認するアドレス |

### レスポンス欄の解説

| フィールド名            | 例の値                                                                  | 説明                         |
| ----------------- | -------------------------------------------------------------------- | -------------------------- |
| `pairs`           |                                                                      | ペアの詳細が含まれているアドレスに基づいたペア一覧： |
| `meta`            |                                                                      | 次のデータを含むオブジェクト：            |
| `base`            | `WEVER`                                                              | 左トークンの名称(例：WEVER)          |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | 左トークンのルートアドレス              |
| `counter`         | `BRIDGE`                                                             | 右トークンの名称(例：BRIDGE)         |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | 右トークンのルートアドレス              |
| `fee`             | `0.300`                                                              | 左/右トークンの取引手数料              |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | 左右ペアのプールアドレス               |
| `tvl`             | `11992480.952892429456`                                              | ペアプールのTVL                  |
| `tvlchange`       | `1.22`                                                               | 過去24時間におけるプール内TVL変化率       |
| `leftLocked`      | `25795814.233390122000`                                              | 左ペア(トークン)のTVL(米ドル)         |
| `leftPrice`       | `0.2322839661557624874057319495`                                     | 左ペアの価格(米ドル)                |
| `rightLocked`     | `644766.509092723000`                                                | 右ペア(トークン)のTVL(米ドル)         |
| `rightPrice`      | `9.293215382388`                                                     | 右ペアの価格(米ドル)                |
| `volume24h`       | 68293.598448021590                                                   | 過去24時間におけるペアの取引量(米ドル)      |
| `volume7d`        | `1549070.057378500757`                                               | 過去7日間におけるペアの取引量(米ドル)       |
| `volumechange24h` | `-44.98`                                                             | 過去24時間の取引量変化率              |
| `fee24h`          | `205.053510628491`                                                   | 過去24時間の手数料総額(米ドル)          |
| `fee7d`           | `4637.831319664494`                                                  | 過去7日間の手数料総額(米ドル)           |
| `feeAllTime`      | `18789.418763913485`                                                 | EVER手数料総額(米ドル)             |
| `offset`          | `0`                                                                  |                            |
| `count`           | `10`                                                                 | 1ページに表示されるペア数              |
| `totalCount`      | `1`                                                                  | 取得したペア数                    |

### 例

```
app.post('/pairs/cross_pairs', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/cross_pairs`,
        data: {
            fromCurrencyAddress: req.body.fromCurrencyAddress,
            toCurrencyAddresses: req.body.toCurrencyAddresses
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

{% swagger method="post" path="/pairs/left/{left}/right/{right}" baseUrl="https://api.flatqube.io/v1" summary="ペアデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "meta": {
    "base": "WEVER",
    "baseAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
    "counterAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
    "counter": "BRIDGE",
    "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
    "fee": "0.3000"
  },
  "tvl": "11992480.952892429456",
  "tvlChange": "1.22",
  "leftLocked": "25795814233390122",
  "leftPrice": "0.2322691452075765631601791831",
  "rightLocked": "644766509092723",
  "rightPrice": "9.292622425991",
  "volume24h": "68293.598448021590",
  "volumeChange24h": "-44.98",
  "volume7d": "1549070.057378500757",
  "fee24h": "205.053510628491",
  "fee7d": "4637.831319664494",
  "feeAllTime": "18789.418763913485"
}
```
{% endswagger-response %}
{% endswagger %}

この機能は、トークンルートアドレスからペアデータ情報を取得するために使用されます。ペアの詳細が使用され、ペアのルートアドレスを使って取得されるべき場合であれば、どこでも使用可能です。

### リクエストパラメータ

左右のパラメータ、つまり特定の通貨アドレスが必要です。\
テストに使用する_WEVERとBRIDGE_の各アドレスです：\
左 = `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`\
\`\`右 = `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`

### レスポンス欄の解説

| フィールド名            | 例の値                                                                  | 説明                         |
| ----------------- | -------------------------------------------------------------------- | -------------------------- |
| `pairs`           |                                                                      | ペアの詳細が含まれているアドレスに基づいたペア一覧： |
| `meta`            |                                                                      | 次のデータを含むオブジェクト：            |
| `base`            | `WEVER`                                                              | 左トークンの名称(例：WEVER)          |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | 左トークンのルートアドレス              |
| `counter`         | `BRIDGE`                                                             | 右トークンの名称(例： BRIDGE)        |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | 右トークンのルートアドレス              |
| `fee`             | `0.300`                                                              | 左/右トークンの取引手数料              |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | 左右ペアのプールアドレス               |
| `tvl`             | `11992480.952892429456`                                              | ペアプールのTVL                  |
| `tvlchange`       | `1.22`                                                               | 過去24時間におけるプール内TVL変化率       |
| `leftLocked`      | `25795814.233390122000`                                              | 左ペア(トークン)のTVL(米ドル)         |
| `leftPrice`       | `0.2322839661557624874057319495`                                     | 左ペアの価格(米ドル)                |
| `rightLocked`     | `644766.509092723000`                                                | 右ペア(トークン)のTVL(米ドル)         |
| `rightPrice`      | `9.293215382388`                                                     | 右ペアの価格(米ドル)                |
| `volume24h`       | 68293.598448021590                                                   | 過去24時間におけるペアの取引量(米ドル)      |
| `volume7d`        | `1549070.057378500757`                                               | 過去7日間におけるペアの取引量(米ドル)       |
| `volumechange24h` | `-44.98`                                                             | 過去24時間の取引量変化率              |
| `fee24h`          | `205.053510628491`                                                   | 過去24時間の手数料総額(米ドル)          |
| `fee7d`           | `4637.831319664494`                                                  | 過去7日間の手数料総額(米ドル)           |
| `feeAllTime`      | `18789.418763913485`                                                 | EVER手数料総額(米ドル)             |

### 例

```
app.post('/pairs/left/:left/right/:right', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/left/${req.params.left}/right/${req.params.right}`
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

{% swagger method="post" path="/pairs/left/{left}/right/{right}/ohlcv" baseUrl="https://api.flatqube.io/v1" summary="Ohlcvペアデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
 {
    "open": "0.024984390565",
    "high": "0.025131270323",
    "low": "0.024980850704",
    "close": "0.025131270323",
    "volume": "249.621417263132",
    "openTimestamp": 1647274428000,
    "closeTimestamp": 1647275606000,
    "timestamp": 1647273600000
  },
  ...
  }
```
{% endswagger-response %}
{% endswagger %}

この機能は、トークンルートアドレスからohlcvペアのデータ情報を取得するために必要です。\
\
例えば、ある一定期間における左ペアの値と比較した、右ペアの値の変化をグラフィックで表示することができます。(例：1 WEVER = 0.02245627 BRIDGE)

### リクエストパラメータ

左のパラメータ、つまり特定の通貨アドレスが必要です。\
テストに使用するWEVERのアドレスです：`0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`

右のパラメータ、つまり特定の通貨アドレスが必要です。\
テストに使用するBRIDGEのアドレスです：\
`0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`

ポストマンテストに使用するデータです：

| フィールド名      | 例の値             | 説明                                                                |
| ----------- | --------------- | ----------------------------------------------------------------- |
| `from`      | `1646741858511` | 期間の開始日時(UNIX形式)(例：1646741858511 または2022年3月8日午後12時17分38秒511 GMT時間) |
| `timeframe` | `H1`            | 価格データの取得期間を時間と日で設定(“H1”, “D1”...)                                 |
| `to`        | `1647346658513` | 期間の開始日時(UNIX形式)(例：1647346658513または2022年3月15日午後12時17分38秒513)       |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### レスポンス欄の解説

| フィールド名           | 例の値                | 説明                                                                                                  |
| ---------------- | ------------------ | --------------------------------------------------------------------------------------------------- |
| `close`          | `0.025131270323`   | 指定期間の終了時間時点での通貨価値(米ドル)                                                                              |
| `closeTimestamp` | `1647275606000`    | 終値の日時(UNIX形式)                                                                                       |
| `high`           | `0.025131270323`   | 指定期間内における最高通貨価格                                                                                     |
| `low`            | `0.024980850704`   | 指定期間内における最低通貨価格                                                                                     |
| `open`           | `0.024984390565`   | 指定期間の開始時間時点での通貨価値(米ドル)                                                                              |
| `openTimestamp`  | `1647274428000`    | 始値の日時(UNIX形式)                                                                                       |
| `timeStamp`      | `1647273600000`    | オープンタイムスタンプのラウンド値(UNIX形式)(例：オープンタイムスタンプが2022年3月8日午後11時25分48秒の場合、GMTに変換すると2022年3月8日午後11時00分00秒になります) |
| `volume`         | `249.621417263132` | 開始時刻と終了時刻間における指定通貨の取引量(米ドル)                                                                         |

### 例

```
 app.post('/pairs/left/:left/right/:right/ohlcv', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/left/${req.params.left}/right/${req.params.right}/ohlcv`,
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
