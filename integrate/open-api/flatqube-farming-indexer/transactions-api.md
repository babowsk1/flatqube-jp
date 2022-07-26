# トランザクションAPI

{% swagger method="post" path="/transactions" baseUrl="http://farming.flatqube.io/v1" summary="トランザクションデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "transactions": [
        {
            "messageHash": "254f05f87ae6d283ce7fc3bcb13919e0a35b2781db54e50046bde369d9a47f2d",
            "transactionHash": "760aa87b1fd7bcbbccae87ab52b187238ac91638f132b048380f711f55e17d4a",
            "kind": "Withdraw",
            "userAddress": "0:f1f1158fcf4f0725a5a53c4d1ac1d37583b36eb4e9ab542d3a288424f6762fdd",
            "poolAddress": "0:f96da52e928cf4d8e54dcec0e7f7fefddfb7592590f05705dcaa9f211102fbc5",
            "tokenAddress": "0:0bf177d4dcc468293502ce81fd9a05285f7621814a705a000020dc15fa8258f8",
            "tokenCurrency": "FLATQUBE-LP-QUBE-WEVER",
            "tokenExec": "9926.264109806000",
            "tvExec": "11289.535028128434",
            "leftExec": "117.580203251916",
            "rightExec": "17702.052927191519",
            "timestampBlock": 1650533932000
        }
    ],
    "totalCount": 1
}
```
{% endswagger-response %}
{% endswagger %}

このメソッドで、トランザクションデータを取得します。

これは、トランザクションタイプ、ユーザーアドレス、プールアドレスなどのリクエストボディパラメータによってフィルタリングされたトランザクション一覧を表示します。\
例えば、特定ユーザーの引き出しトランザクションに関する詳細情報を表示します。

### 必要なデータ

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名                 | 例の値                                                                                                                                                  | 説明                                       |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| eventTypes             | deposit                                                                                                                                              | トランザクションタイプ(預け入れ、引き出し)                   |
| limit                  | 10                                                                                                                                                   | 返送すべき最大トランザクション数                         |
| poolAddress            | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0                                                                                   | トランザクションが処理されているファーミングプールのアドレス           |
| rootAddress            | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2                                                                                   | LPトークンのアドレス                              |
| rootTokenAmountGe      | 12400                                                                                                                                                | LPトークン量がこの値以上であるトランザクションをフィルタリングするときの値   |
| rootTokenAmountLe      | 12600                                                                                                                                                | LPトークン量がこの値以下であるトランザクションをフィルタリングするときの値   |
| timestampBlockGe       | 1647590400000                                                                                                                                        | ブロックタイムスタンプがこれ以上のトランザクションをフィルタリングするときの日時 |
| timestampBlockLe       | 1648195200000                                                                                                                                        | ブロックタイムスタンプがこれ以下のトランザクションをフィルタリングするときの日時 |
| tvGe                   | 5800                                                                                                                                                 | 合計額がこの値以上のトランザクションをフィルタリングするときの値         |
| tvLe                   | 6500                                                                                                                                                 | 合計額がこの値以下のトランザクションをフィルタリングするときの値         |
| userAddress            | 0:0e7ebac7bdfcec9edb511113774c75e8c4949d2c5ab2b903837bd2ff04128d68                                                                                   | ユーザーアドレス                                 |
| whiteCurrencyAddresses | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d, 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1               | -                                        |
| whiteListUri           | [https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json](https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json) | ホワイトリストへのパス                              |

### レスポンス欄の解説

| フィールド名          | 例の値                                                                | 説明                        |
| --------------- | ------------------------------------------------------------------ | ------------------------- |
| totalCount      | 2                                                                  | 1つのプールにおけるトランザクション合計数     |
| Transactions    | -                                                                  | 次のデータを含むトランザクション一覧        |
| kind            | Withdraw                                                           | トランザクションタイプ(預け入れ、請求、引き出し) |
| leftExec        | null                                                               | トランザクションに参加している左の通貨量      |
| messegeHash     | 80056a0cb8ea3a2710edd823b9250d8ee717c825079c50667d4c84824138f2d6   | トランザクションメッセージのハッシュ        |
| poolAddress     | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | プールアドレス                   |
| rightExec       | 148.559845816278                                                   | トランザクションに参加している右の通貨量      |
| timestampBlock  | 1649355777000                                                      | トランザクションブロックの生成日時         |
| tokenAddress    | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2 | LPトークンアドレス                |
| tokenCurrency   | FLATQUBE-LP-WEVER-BRIDGE                                           | LPトークンシンボル                |
| tokenExec       | 6333.372380447000                                                  | トランザクションのトークン量            |
| transactionHash | b78457c3ca523321bed353567954ded6cd8af94dfff32aae7098f33cd9603bfa   | トランザクションのハッシュコード          |
| tvExec          | 2719.899465109213                                                  | 取引金額合計(米ドル)               |
| userAddress     | 0:f1f1158fcf4f0725a5a53c4d1ac1d37583b36eb4e9ab542d3a288424f6762fdd | トランザクションを開始するユーザーのアドレス    |

### 例

```
 app.post('/transactions', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/transactions`,
        data: {
            eventTypes: req.body.eventTypes,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            poolAddress: req.body.poolAddress,
            rootAddresses: req.body.rootAddresses,
            rootTokenAmountGe: req.body.rootTokenAmountGe,
            rootTokenAmountLe: req.body.rootTokenAmountLe,
            timestampBlockGe: req.body.timestampBlockGe,
            timestampBlockLe: req.body.timestampBlockLe,
            tvGe: req.body.tvGe,
            tvLe: req.body.tvLe,
            userAddress: req.body.userAddress,
            whiteCurrencyAddresses: req.body.whiteCurrencyAddresses,
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
