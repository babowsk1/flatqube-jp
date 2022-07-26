# CMC API

{% swagger method="get" path="" baseUrl="https://api.flatqube.io/v1/cmc/dex" summary="CMC DEX プール情報" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2_0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6": {
            "base_id": "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2",
            "base_name": "Tether",
            "base_symbol": "USDT",
            "quote_id": "0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6",
            "quote_name": "USD Coin",
            "quote_symbol": "USDC",
            "last_price": "1.001259244956",
            "base_volume": "2210.44204800",
            "quote_volume": "2213.22553600"
    },
    "0:0cfa60f9454b1b619938c4da6a138b1cc62da937b3f6c0506405daf2a88e0115_0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d": {
            "base_id": "0:0cfa60f9454b1b619938c4da6a138b1cc62da937b3f6c0506405daf2a88e0115",
            "base_name": "EUR-Fiat-Based",
            "base_symbol": "EUPI",
            "quote_id": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
            "quote_name": "Wrapped EVER",
            "quote_symbol": "WEVER",
            "last_price": "5.547157916853",
            "base_volume": "359.90566477",
            "quote_volume": "1996.453557649000"
    },
    ...
}
```
{% endswagger-response %}
{% endswagger %}

この機能を使用すると、DEXプールに関するあらゆる情報を取得できます。

全てのDEXプール、そのペアやそれらに関する必要な情報を一覧化できます。

### リクエストパラメータ

_パラメータは必要ありません_

### レスポンス欄の解説

| フィールド名         | 例の値                                                                  | 説明                                          |
| -------------- | -------------------------------------------------------------------- | ------------------------------------------- |
| `base_id`      | `0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2` | 特定のdexプールにあるベーストークンのルートアドレス                 |
| `base_name`    | `Tether`                                                             | ベーストークンの正式名称                                |
| `base_symbol`  | `USDT`                                                               | ベーストークンのシンボル                                |
| `quote_id`     | 0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6   | プールにあるクォートトークンのルートアドレス                      |
| `quote_name`   | `USD Coin`                                                           | クォートトークンの正式名称                               |
| `quote_symbol` | `USDC`                                                               | クォートトークンのシンボル                               |
| `last_price`   | `1.001259244956`                                                     | 1クォートトークンにおける1ベーストークンの価格(例：1USDT＝1.001USDC) |
| `base_volume`  | `2210.44204800`                                                      | ベーストークンの取引量(米ドル)                            |
| `quote_volume` | `2213.22553600`                                                      | クォートトークンの取引量(米ドル)                           |

### 例

```javascript
  app.get('/cmc/dex', (req, res) => {
        axios({
            method: 'get',
            url: liveApiUrl + '/cmc/dex'
          })
        .then(function (response) {
            res.send(response.data)
        })
        .catch(function(error){
            console.error(error)
            res.send('Error')
        })
  })
```

{% swagger method="get" path="/cmc/farming" baseUrl="https://api.flatqube.io/v1" summary="CMC DEXファーミングプール情報" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "provider": "FlatQube",
    "provider_logo": "https://flatqube.io/favicon.svg",
    "provider_URL": "https://flatqube.io",
    "links": [],
    "pools": [{
                "name": "SOON/WEVER",
                "pair": "SOON/WEVER",
                "pairLink": "https://flatqube.io/farming/0:5b297ebf0d4baa84e5e5f2cff61f3563fa94e62e8c93d5a2fd19145d72007bf3",
                "logo": "https://flatqube.io/favicon.svg",
                "poolRewards": ["SOON", "COLA", "BAPBAPA", "GRE"],
                "apr": "3.0815",
                "totalStake": "114846.005396701372"
            }, {
                "name": "USDT/DUSA",
                "pair": "USDT/DUSA",
                "pairLink": "https://flatqube.io/farming/0:2ff5db6e886e337c921154f3de9b77cfcadd1940c84b4f3b97c312c069cd7ea0",
                "logo": "https://flatqube.io/favicon.svg",
                "poolRewards": ["DUSA"],
                "apr": "97.9022",
                "totalStake": "53838.449198250683"
            }, {
                "name": "WEVER/BRIDGE",
                "pair": "WEVER/BRIDGE",
                "pairLink": "https://flatqube.io/farming/0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0",
                "logo": "https://flatqube.io/favicon.svg",
                "poolRewards": ["BRIDGE", "QUBE"],
                "apr": "0.5353",
                "totalStake": "11763741.699148025624"
            },
            ...
    }
```
{% endswagger-response %}
{% endswagger %}

この機能は、ファーミングプール情報を取得するためのものです：

### リクエストパラメータ

_パラメータは必要ありません_

### レスポンス欄の解説

| フィールド名          | 例の値                                                                                                                                                                                                | 説明                                             |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| `provider`      | `FlatQube`                                                                                                                                                                                         | ファーミングプロバイダー                                   |
| `provider_logo` | [`https://flatqube.io/favicon.svg`](https://flatqube.io/favicon.svg)\`\`                                                                                                                           | プロバイダーロゴプロバイダーへのパス                             |
| `url`           | https://flatqube.io                                                                                                                                                                                | プロバイダーへのURL                                    |
| `links`         |                                                                                                                                                                                                    |                                                |
| `pools`         |                                                                                                                                                                                                    | プロバイダーで利用可能なプールの一覧表には、各プールに関する次の情報が含まれています     |
| `name`          | `WEVER/BRIDGE`                                                                                                                                                                                     | プール名称(左ペア/右ペア)                                 |
| `pair`          | `WEVER/BRIDGE`                                                                                                                                                                                     | 指定されたプールで、どのトークンがペアになっているかについての情報              |
| `pairLink`      | [`https://flatqube.io/farming/0:5b297ebf0d4baa84e5e5f2cff61f3563fa94e62e8c93d5a2fd19145d72007bf3`](https://flatqube.io/farming/0:5b297ebf0d4baa84e5e5f2cff61f3563fa94e62e8c93d5a2fd19145d72007bf3) | そのプールに関する詳細を表示し、ファーミングを開始できるファーミングプールへのURL     |
| `logo`          | [`https://flatqube.io/favicon.svg`](https://flatqube.io/favicon.svg)\`\`                                                                                                                           |                                                |
| `poolRewards`   | `BRIDGE, QUBE`                                                                                                                                                                                     | そのプールで行ったファーミングの対価として与えられるトークン(例：BRIDGE、QUBE等) |
| `apr`           | `97.9022`                                                                                                                                                                                          | そのプールで行ったファーミングのAPR(年率)                        |
| `totalStake`    | `53838.449198250683`                                                                                                                                                                               | 現在のプールTVL(米ドル)                                 |

### 例

```
app.get('/cmc/farming', (req, res) => {
    axios({
        method: 'get',
        url: liveApiUrl + '/cmc/farming'
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```
