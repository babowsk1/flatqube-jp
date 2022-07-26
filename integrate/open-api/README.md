---
description: FlatQubeは、アプリケーションのデータ取得を容易にするために、読み取り専用のAPIを提供しています。
---

# オープンAPI

***

{% hint style="warning" %}
**未完成の記事**\
\
このページは作成中です。早く完成させるために最善を尽くしています。 ご協力いただける方は、hello@broxus.com までお気軽にご連絡ください。
{% endhint %}

以下のAPIは、FlatQube自身がユーザーインターフェイスを容易にするために使用します。\
添付されているSwaggerスキームをご参照ください。

## FlatQubeインデクサー

{% embed url="https://api.flatqube.io/v1/swagger.yaml" %}
Swagger scheme
{% endembed %}

## ファーミングインデクサー

{% embed url="https://farming.flatqube.io/v1/swagger.yaml" %}
Swagger scheme
{% endembed %}

## 関数呼び出し

{% hint style="info" %}
以下で、様々な関数呼び出しとその使用例についてご紹介しています。

以下のように、APIコールメソッドは全て2つのセクションに分けられています：FlatQube Dex Indexer (CMC、通貨、ペア、トランザクションAPI)\
FlatQube Farming Indexer (ファーミングプール、トランザクション、グラフィックスAPI)
{% endhint %}

## Node.js コードスニペット

以下の例で使用しているライブラリです：

* [_Express (Node.js)_ ](https://expressjs.com/en/4x/api.html)\_\_
* [_**Axios**_](https://axios-http.com/docs/intro)
* [_**body-parser**_](https://www.npmjs.com/package/body-parser)
