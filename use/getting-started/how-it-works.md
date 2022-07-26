---
description: FlatQubeの基本を学ぶことで、その背景にあるプロセスをより深く理解できます。
---

# 仕組み

## 基本

FlatQubeは、主要マーケットソリューションから着想を得た自動流動性プロトコルです。一定のプロダクト式に基づいており、ノンカストディアル、分散型、検閲に強い安全な方法で流動性を提供し、トークンペアを交換できます。

Uniswapや他のEthereumベースのDEXとは異なり、FlatQubeは[Everscaleネットワーク](https://everscale.network/)上で機能しているため、その非同期処理、ハイスループット、高速ファイナリティのメリットを享受できます。

FlatQubeは、[Apache 2.0](https://github.com/broxus/ton-dex/blob/master/LICENSE)の下でライセンスされたオープンソースソフトウェアです。

## 流動性プール

FlatQubeはスマートコントラクトの集合体で運営されており、その主体である[ペア](https://github.com/broxus/ton-dex/blob/master/contracts/DexPair.sol)は、2つの[TIP-3.1トークン](../tokens/concepts/tokens-we-use.md#tokens-standard)の埋蔵量からなる流動性プールを管理しています。

プールトークン(LPトークン)と引き換えに、各基本トークンを相当数を預けることで、誰でもプールの流動性プロバイダー(LP)になることができます。これらのトークンは、総埋蔵量に比例したLPシェアを追跡し、いつでも原資産と交換できます。

{% hint style="info" %}
参照：[LPトークン量の計算方法](../pools/how-to/calculate-the-amount-of-lp-tokens.md)
{% endhint %}

FlatQubeは、Everscaleの特殊性のおかげで、他のDEXとは異なり、提供前のポジションを蓄積するために[DEXアカウント](https://github.com/broxus/ton-dex/blob/master/contracts/DexAccount.sol)という中間契約を使用します。LP(流動性プロバイダー)はプールに流動性を供給するために、DEXアカウントに両方の原資産を預ける必要があります。&#x20;

{% hint style="info" %}
FlatQubeはプール内に供給された資産のうち、必要な部分を自動的に交換することで、片面的な流動性提供をサポートします。[続きを読む](../pools/how-to/add-liquidity.md#one-sided-liquidity-provision)&#x20;
{% endhint %}

## カーテンの裏に隠された計算

ペアは自動化されたマーケットメーカーとして機能し、「定量的計算式」が守られている限り、一方のトークンと他方のトークンを受け入れる準備ができています。この式は`x * y = k`であり、取引に関わらず、ペアの準備金残高（`xと` `y`）の積（`k`）は一定です。`k`は取引の基準フレームから変化しないため、_不変量_と呼ばれています。この式には、(準備金に対して)大きな取引は小さな取引より、指数関数的に悪いレートで処理されるという望ましい性質があります。

実際、FlatQubeは取引手数料を0.30%にすることで積立金を増やし、結果的に不変量が増加します。これはLPの繰延利益として機能し、LPがプールトークンをバーンして、総発行量のうち自分の取り分を引き出す際に受け取ります。

このため、資産の相対価格は取引によってのみ変化し、裁定取引の機会を得られます。このような仕組みにより、DEXの価格は、常に市場清算価格に向かって推移します。
