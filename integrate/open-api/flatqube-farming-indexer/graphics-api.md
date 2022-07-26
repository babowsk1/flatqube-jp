# グラフィックスAPI

{% swagger method="post" path="/graphic/tvl" baseUrl="http://farming.flatqube.io/v1" summary="ファーミングプールTVLグラフィックデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
[
    {
        "data": "19315318.324282999059",
        "timestamp": 1652853600000
    },
...
]
```
{% endswagger-response %}
{% endswagger %}

このメソッドで、ファーミングプールTVLグラフィックデータを取得します。

ある期間におけるTVL変化(米ドル)のグラフィック表示に使用されます。リクエストに必要なデータは、ファーミングプールのアドレスと、リクエストボディで設定されているTVL変化の追跡期間です。

### リクエストパラメータ

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名             | 例の値                                                                | 説明                         |
| ------------------ | ------------------------------------------------------------------ | -------------------------- |
| farmingPoolAddress | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | 希望するファーミングプールのアドレス         |
| from               | 1646741858511                                                      | 望期間の開始日時(UNIX形式)           |
| timeframe          | H1                                                                 | <p>期間のステップを<br>時間と日で設定</p> |
| to                 | 1647346658513                                                      | 期間の終了日時(UNIX形式)            |

### レスポンス欄の解説

| フィールド名    | 例の値                   | 説明                               |
| --------- | --------------------- | -------------------------------- |
| data      | 19315318.324282999059 | ある瞬間における、1つのファーミングプール内の合計残高(米ドル) |
| timestamp | 1652853600000         | データが取得される瞬間の日時(UNIX形式)           |

### 例

```
 app.post('/graphic/tvl', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/graphic/tvl`,
        data: {
            farmingPoolAddress: req.body.farmingPoolAddress,
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

{% swagger method="post" path="/graphic/apr" baseUrl="http://farming.flatqube.io/v1" summary="ファーミングプールAPRグラフィックデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful response " %}
```
[
    {
        "data": "74.5300",
        "timestamp": 1652878800000
    },
    ...
]
```
{% endswagger-response %}
{% endswagger %}

このメソッドで、ファーミングプールAPRグラフィックデータを取得します。

ある期間におけるAPR変化率のグラフィック表示に使用されます。リクエストに必要なデータは、ファーミングプールのアドレスと、リクエストボディで設定されているAPR変化率の追跡期間です。

### リクエストパラメータ

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名             | 例の値                                                               | 説明                            |
| ------------------ | ----------------------------------------------------------------- | ----------------------------- |
| farmingPoolAddress | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff | 希望するファーミングプールのアドレス            |
| from               | 1646741858511                                                     | 期間の開始日時(UNIX形式)               |
| timeframe          | H1                                                                | <p>期間のステップを</p><p>時間と日で設定</p> |
| to                 | 1647346658513                                                     | 期間の終了日時(UNIX形式)               |

### レスポンス欄の解説

| フィールド名    | 例の値           | 説明                            |
| --------- | ------------- | ----------------------------- |
| data      | 74.5300       | ある瞬間における、1つのファーミングプール内のAPR(%) |
| timestamp | 1652878800000 | データが取得される瞬間の日時(UNIX形式)        |

### 例

```
 app.post('/graphic/apr', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/graphic/apr`,
        data: {
            farmingPoolAddress: req.body.farmingPoolAddress,
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
