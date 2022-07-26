# トランザクションAPI

{% swagger method="post" path="/transactions" baseUrl="https://api.flatqube.io/v1" summary="トランザクションデータ" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "transactions": [
        {
            "messageHash": "beb4a1ba4cbf5d82bef26aee4020234100efe893d12d206a8b802a50cf0e19ed",
            "transactionHash": "a44818ac6ff16d485f65012ee1ff1faca9cf0182982f4e6aaf5fd0b706b45b2b",
            "left": "WBTC",
            "right": "BRIDGE",
            "tv": "47.866903714982",
            "leftValue": "120119",
            "rightValue": "5207609968",
            "userAddress": "0:41dc520061a68ba82de79c4748c3bfdb93bb7443203394890dad19905dbec8fd",
            "poolAddress": "0:ab39f6f37b9eb96f187199ff7f88745efe99bfa7624691f9f7d1e7713b6bc478",
            "leftAddress": "0:2ba32b75870d572e255809b7b423f30f36dd5dea075bd5f026863fceb81f2bcf",
            "rightAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
            "timestampBlock": 1649965345,
            "createdAt": 1649965352915,
            "eventType": "swaplefttoright",
            "fee": "0.00000361",
            "feeCurrency": "WBTC"
        },
...
}
```
{% endswagger-response %}
{% endswagger %}

この機能は、必要なパラメータでフィルタリングされた特定ユーザーのトランザクションデータを取得するために必要です。

### リクエストパラメータ

ボディが必要です。ポストマンテストに使用するデータです：

| フィールド名              | 例の値                                                                        | 説明                                          |
| ------------------- | -------------------------------------------------------------------------- | ------------------------------------------- |
| `createdAtGe`       | `0`                                                                        | UNIX形式の日時で、その日時の後または間に作成されたトランザクションをフィルタリング |
| `createdAtLe`       | `0`                                                                        | UNIX形式の日時で、その日時の前または間に作成されたトランザクションをフィルタリング |
| `currencyAddress`   | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`       | トランザクションペアにおける左通貨のルートアドレス                   |
| `currencyAddresses` | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`       | トランザクションペアにおける右通貨のルートアドレス                   |
| `eventType`         | `swaplefttoright`                                                          | トランザクションタイプ(スワップ、追加、削除)                     |
| `leftAmountGe`      | `0.194319663088308553962886430`                                            | トランザクションペアの左が指定値以上                          |
| `leftAmountLe`      | `9.029870729776`                                                           | トランザクションペアの左が指定値以下                          |
| `limit`             | `0`                                                                        | 数量制限                                        |
| `offset`            | `0`                                                                        |                                             |
| `ordering`          | `blocktimeascending`                                                       | トランザクション時間(昇順・降順)                           |
| `poolAddress`       | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06`       | ペアのプールアドレス                                  |
| `rightAmountGe`     | `7.029870729776`                                                           | トランザクションペアの右が指定値以上                          |
| `rightAmountLe`     | `9.029870729776`                                                           | トランザクションペアの右が指定値以下                          |
| `timestampBlockGe`  | `0`                                                                        | この値以上のブロックのフィルタータイムスタンプ                     |
| `timestampBlockLe`  | `0`                                                                        | この値以下のブロックのフィルタータイムスタンプ                     |
| `tvGe`              | `8955040.156573434959`                                                     | 合計額がこの値以上のトランザクションをフィルタリング                  |
| `tvLe`              | `8955043.156573434959`                                                     | 合計額がこの値以下のトランザクションをフィルタリング                  |
| `userAddress`       | `0:3aeefed73a08979d5f7d489e7fe06f0d20a433e27f81b70a4e2e0d7f3968ede8`       | トランザクションを開始するユーザーのアドレス                      |
| `whiteListUri`      | `https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json` | ホワイトリストへのパス                                 |

### レスポンス欄の解説

| フィールド名            | 例の値                                                                  | 説明                      |
| ----------------- | -------------------------------------------------------------------- | ----------------------- |
| `count`           | 10                                                                   | 1ページに表示されるトランザクション数     |
| `offset`          | 0                                                                    |                         |
| `totalCount`      | 4132                                                                 | 必要な全トランザクション数           |
| `transactions`    | -                                                                    | 取引成立日時(UNIX形式)          |
| `createdAt`       | `1649965461706`                                                      | 取引成立日時(UNIX形式)          |
| `eventType`       | `deposit`                                                            | トランザクションタイプ(スワップ、追加、削除) |
| `fee`             | `null`                                                               | トランザクション手数料             |
| `feeCurrency`     | `null`                                                               | トランザクション手数料の通貨          |
| `left`            | `WEVER`                                                              | 右ペアの通貨                  |
| `leftAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | 左ペアのルートアドレス             |
| `leftValue`       | `915417342444`                                                       | 左ペア値                    |
| `messageHash`     | `c264d77bf677742d3d0c8065b92d1bf6137444917e20fafebe9a6b7f3376bd24`   | トランザクションメッセージのハッシュコード   |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | ペアプールのアドレス              |
| `right`           | `BRIDGE`                                                             | 右ペアの通貨                  |
| `rightAddress`    | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | 右ペアのルートアドレス             |
| `rightValue`      | `22933551212`                                                        | 右ペア値                    |
| `timestampBlock`  | `1649965452`                                                         | ブロック生成日時                |
| `transactionHash` | `49bf48242de460facac859896ad9987d065d8bb15395f14ca907020cff32aba9`   | トランザクションのハッシュ           |
| `tv`              | `421.597659752853`                                                   | 取引金額合計(米ドル)             |
| `userAddress`     | `0:b2475c0716d754fba88eb28e12b45e6f636729f96270aebb859730af86182cf4` | トランザクションを作成したユーザーのアドレス  |

### 例

```
 app.post('/transactions', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/transactions`,
        data: {
            createdAtGe: req.body.createdAtGe,
            createdAtLe: req.body.createdAtLe,
            currencyAddress: req.body.currencyAddress,
            currencyAddresses: req.body.currencyAddresses,
            eventType: req.body.eventType,
            leftAmountGe: req.body.leftAmountGe,
            leftAmountLe: req.body.leftAmountLe,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            poolAddress: req.body.poolAddress,
            rightAmountGe: req.body.rightAmountGe,
            rightAmountLe: req.body.rightAmountLe,
            timestampBlockGe: req.body.timestampBlockGe,
            timestampBlockLe: req.body.timestampBlockLe,
            tvGe: req.body.tvGe,
            tvLe: req.body.tvLe,
            userAddress: req.body.userAddress,
            whiteListUri: req.body.whiteListUri,
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error') }) })
```
