# ファーミングプールAPI

{% swagger method="post" path="/farming_pools" baseUrl="http://farming.flatqube.io/v1" summary="ファーミングプールデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "pools_info": [
        {
            "pool_address": "0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0",
            "left_address": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
            "right_address": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
            "left_currency": "WEVER",
            "right_currency": "BRIDGE",
            "tvl": "17826322.032214433830",
            "tvl_change": "1.54",
            "apr": "59.7900",
            "apr_change": "-0.62",
            "share": "0",
            "user_token_balance": "0",
            "is_low_balance": false,
            "pool_owner_address": "0:a2b489a30c88648ab4bf98c2ba9d07c363c9d93e72a43a0625ff4644524582c6",
            "token_root_address": "0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2",
            "token_root_currency": "FLATQUBE-LP-WEVER-BRIDGE",
            "token_root_scale": 9,
            "farm_start_time": 1653004800000,
            "farm_end_time": null,
            "is_active": true,
            "reward_token_root_info": [
                {
                    "reward_root_address": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
                    "reward_currency": "BRIDGE",
                    "reward_scale": 9
                },
                {
                    "reward_root_address": "0:9f20666ce123602fd7a995508aeaa0ece4f92133503c0dfbd609b3239f3901e2",
                    "reward_currency": "QUBE",
                    "reward_scale": 9
                }
            ]
}
```
{% endswagger-response %}
{% endswagger %}

このメソッドは、目的のファーミングプール一覧、例えばユーザーがお気に入り登録したファーミングプール一覧を表示するために使用します。\
一覧は、左右の通貨とトークンアドレス、ファーミングプールルートアドレス、合計ロック額の変化、プールアクティビティなどのリクエストボディパラメータでフィルタリング可能です。

### リクエストパラメータ

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名                | 例の値                                                                                                                                    | 説明                                        |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| aprGe                 | 52.6300                                                                                                                                | APRがこの値以上のプールをフィルタリングするときの値               |
| aprLe                 | 60                                                                                                                                     | APRがこの値以下のプールをフィルタリングするときの値               |
| favoritePoolAddresses | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0                                                                     | お気に入り登録されたアドレス                            |
| isActive              | true                                                                                                                                   | プールがアクティブな場合はtrue、そうでない場合はfalse           |
| isAwaitingStart       | true                                                                                                                                   | プールがファーミングの開始を待っている場合はtrue、待っていない場合はfalse |
| isLowBalance          | false                                                                                                                                  | 残高が少ない場合はtrue、少なくない場合はfalse               |
| isWithMyFarming       | true                                                                                                                                   | はいの場合はtrue、いいえの場合はfalse                   |
| leftAddress           | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d                                                                     | 左通貨のルートアドレス                               |
| leftCurrency          | WEVER                                                                                                                                  | 左通貨のシンボル                                  |
| limit                 | 0                                                                                                                                      | 1ページあたりのプール表示数                            |
| offset                | 0                                                                                                                                      | オフセット                                     |
| rightAddress          | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1                                                                     | 右通貨のルートアドレス                               |
| rightCurrency         | BRIDGE                                                                                                                                 | 右通貨のシンボル                                  |
| rottAddress           | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1, 0:9f20666ce123602fd7a995508aeaa0ece4f92133503c0dfbd609b3239f3901e2 | LPアドレス                                    |
| tvlGe                 | 120177899                                                                                                                              | TVLがこの値以上のプールをフィルタリングするときの値               |
| tvlLe                 | 12217899                                                                                                                               | TVLがこの値以下のプールをフィルタリングするときの値               |
| userAddress           | 0:102cf118b6875d201a3011d5dc17a358ee4d4333ad7e167824515171ed8f6f63                                                                     | ユーザーアドレス                                  |

### レスポンス欄の解説

| フィールド名                    | 例の値                                                                | 説明                                    |
| ------------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| Pools\_info               | -                                                                  | 以下の情報が含まれた利用できるプール一覧                  |
| favorite\_pools\_info     | -                                                                  | 以下の情報が含まれ、ユーザーがお気に入り登録したファーミングプール一覧   |
| apr                       | 205                                                                | 年率                                    |
| apr\_change               | -0.50                                                              | 過去24時間におけるAPRの変化                      |
| farm\_end\_time           | null                                                               | 特定のプールにおけるファーミング終了日時                  |
| farm\_start\_time         | 1649289600000                                                      | 特定のプールにおけるファーミング開始日時                  |
| is\_active                | true                                                               | プールがアクティブな場合はtrue、そうでない場合はfalse       |
| is\_low\_balance          | false                                                              | 残高が少ない場合はtrue、少なくない場合はfalse           |
| left\_address             | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d | プールにある左通貨のルートアドレス                     |
| left\_currency            | WEVER                                                              | 左通貨のシンボル (例：WEVER)                    |
| pool\_address             | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | 現在のプールアドレス                            |
| pool\_owner\_address      | 0:a2b489a30c88648ab4bf98c2ba9d07c363c9d93e72a43a0625ff4644524582c6 | プールを作成したユーザーのアドレス                     |
| reward\_token\_root\_info | -                                                                  | リワードトークンに関する以下の情報が含まれたリワードトークン一覧      |
| reward\_currency          | BRIDGE                                                             | リワードトークンのシンボル                         |
| reward\_root\_address     | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | 特定のリワードトークンのルートアドレス                   |
| reward\_scale             | 9                                                                  | リワード量とこの値を掛け合わせることで、正しい数量を得る          |
| right\_address            | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | プールにある右通貨のルートアドレス                     |
| right\_currency           | BRIDGE                                                             | 右通貨のシンボル (例： BRIDGE)                  |
| share                     | 0                                                                  | プールへの貢献のためにユーザーが共有したトークンの量            |
| token\_root\_address      | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2 | 流動性プールのアドレス                           |
| token\_root\_currency     | FLATQUBE-LP-WEVER-BRIDGE                                           | 流動性プールの名称(例：FLATQUBE-LP-WEVER-BRIDGE) |
| tvl                       | 17826322.032214433830                                              | そのプールのTVL                             |
| tvl\_change               | 1.54                                                               | 過去24時間のTVL変化率                         |
| user\_token\_balance      | 0                                                                  | FlatQubeアカウントを共有しているユーザーの残高           |
| favorite\_total\_count    | 4                                                                  | ユーザーがお気に入り登録したファーミングプールの総数            |

### 例

```
app.post('/farming_pools', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/farming_pools`,
        data: {
            aprGe: req.body.aprGe,
            aprLe: req.body.aprLe,
            favoritePoolAddresses: req.body.favoritePoolAddresses,
            isActive: req.body.isActive,
            isAwaitingStart: req.body.isAwaitingStart,
            isLowBalance: req.body.isLowBalance,
            isWithMyFarming: req.body.isWithMyFarming,
            leftAddress: req.body.leftAddress,
            leftCurrency: req.body.leftCurrency,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            rightAddress: req.body.rightAddress,
            rightCurrency: req.body.rightCurrency,
            rootAddresses: req.body.rootAddresses,
            tvlGe: req.body.tvlGe,
            tvlLe: req.body.tvlLe,
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

{% swagger method="post" path="/farming_pools/{farming_pool_address}" baseUrl="http://farming.flatqube.io/v1" summary="ファーミングプールデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

このメソッドでは、ファーミングプールアドレスから特定のファーミングプールデータを取得します。

年率、プール残高、左右の通貨とアドレス、合計ロック額など目的のファーミングプールとその詳細を表示します。

### リクエストパラメータ

ファーミングプールアドレスパラメータ、つまり特定のファーミングプールアドレスが必要です。\
テストに使用する値: `0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0`

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名           | 例の値                                                                | 説明       |
| ---------------- | ------------------------------------------------------------------ | -------- |
| afterZeroBalance | true                                                               | -        |
| userAddress      | 0:102cf118b6875d201a3011d5dc17a358ee4d4333ad7e167824515171ed8f6f63 | ユーザーアドレス |

### レスポンス欄の解説

| フィールド名                    | 例の値                                                                | 説明                                       |
| ------------------------- | ------------------------------------------------------------------ | ---------------------------------------- |
| apr                       | 59.7                                                               | 現在のプールにおける年率                             |
| apr\_change               | -0.62                                                              | 過去24時間におけるAPRの変化                         |
| farm\_end\_time           | null                                                               | 特定のプールにおけるファーミング終了日時(UNIX形式)             |
| farm\__start\_time_       | 1653004800000                                                      | 特定のプールにおけるファーミング開始日時(UNIX形式)             |
| history\_info             | -                                                                  | このプールにおけるユーザーの次のような活動情報：                 |
| left\_amount              | 0                                                                  | 右通貨のリワード額                                |
| right\_amount             | 0                                                                  | 右通貨のリワード額                                |
| usdt\_amount              | 0                                                                  | USDTの合計額                                 |
| is\_active                | true                                                               | プールがアクティブの場合はtrue、そうでない場合はfalse          |
| is\__low\_balance_        | false                                                              | 残高が少ない場合はtrue、少なくない場合はfalse              |
| left\_address             | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d | プールにある左通貨のルートアドレス                        |
| left\_balance             | 41429655.89348116                                                  | プールにある左通貨の残高合計                           |
| left\_currency            | WEVER                                                              | 左通貨のシンボル                                 |
| pool\_address             | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | 現在のプールアドレス                               |
| pool\_balance             | 37424521.838044951                                                 | あるプール内のLPトークンの総残高                        |
| pool\_info                | -                                                                  | 特定のプールに関する以下のデータが含まれています:                |
| rounds\_info              | -                                                                  | プール内のファーミングラウンド一覧と、それらに関する以下の情報が含まれています： |
| end\_time                 | 1650412800                                                         | ラウンド終了日時(UNIX形式)                         |
| reward\_info              | -                                                                  | リワードトークン一覧とリワードに関する追加情報が含まれています：         |
| rewardPerSec              | 0.0050                                                             | 1秒間にリワードとして配布されるトークンの数量                  |
| rewardTokenRootAddress    | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | リワードトークンのシンボル                            |
| rewardTokenScale          | 9                                                                  | あるトークンのルートアドレス                           |
| start\_time               | 1650412800                                                         | ラウンド開始日時(UNIX形式)                         |
| vesting\_period           | 10368000                                                           | 権利確定時期                                   |
| versting\_ratio           | 1000                                                               | 権利確定に回される報酬割合                            |
| pool\__owner\_address_    | 0:a2b489a30c88648ab4bf98c2ba9d07c363c9d93e72a43a0625ff4644524582c6 | プールを作成したユーザーのアドレス                        |
| reward\_token\_root\_info | -                                                                  | リワードトークン一覧と、それらに関する以下の情報：                |
| reward\_currency          | BRIDGE                                                             | リワードトークンのシンボル                            |
| reward\__per\_second_     | 0.0050                                                             | 1秒間にリワードとして配布されるトークンの数量                  |
| reward\__root\_address_   | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | 特定のリワードトークンのルートアドレス                      |
| reward\__token\_scale_    | 9                                                                  | リワード量のスケーリングに使用する値                       |
| right\_address            | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | プール内にある右通貨のルートアドレス                       |
| right\_balance            | 815476.108391363066                                                | プール内における左通貨の合計残高                         |
| right\_currency           | BRIDGE                                                             | 右通貨のシンボル                                 |
| share                     | 0                                                                  | プールへの貢献のためにユーザーが共有したトークンの量               |
| share\_change             | 0                                                                  | 過去24時間のシェア推移率                            |
| token\__root\_address_    | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2 | 流動性プールのアドレス                              |
| token\__root\_scale_      | 9                                                                  | LPトークン量のスケーリングに使用する値                     |
| _token\_root\_currency_   | FLATQUBE-LP-WEVER-BRIDGE                                           | 流動性プールの名称                                |
| tvl                       | 17826322.032214433830                                              | そのプールのTVL                                |
| tvl\_change               | 1.54                                                               | 過去24時間のTVL変化率                            |
| user\__token\_balance_    | 0                                                                  | FlatQubeアカウントを共有しているユーザーのLPトークン残高        |
| user\__usdt\_balance_     | 0                                                                  | FlatQubeアカウントを共有しているユーザーの残高(USDT)        |

### 例

```
 app.post('/farming_pools/:farming_pool_address', (req, res) => {
    console.log(`Request body data: ${req.params.farming_pool_address}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/farming_pools/${req.params.farming_pool_address}`,
        data: {
            afterZeroBalance: req.body.afterZeroBalance,
            userAddress: req.body.userAddress
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
