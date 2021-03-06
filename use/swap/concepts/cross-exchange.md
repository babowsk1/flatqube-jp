# クロスエクスチェンジ

ご存知の通り、FlatQube上で、あるトークンを別のトークンと交換する機能は、[プール内の流動性](../../pools/)によって提供されています。\
対応するプールに十分な流動性がない場合、または必要なプールが存在しない場合、**クロスエクスチェンジ**が用いられます。\
クロスエクスチェンジの本質は、一度に複数の流動性プールとやり取りすることです：\
例えば、トークンAとトークンBを交換したいが、対応するプールが存在しないとします。この場合、FlatQubeはトークンAをトークンCに交換し（AとCのプールのやり取り）、トークンCをトークンBに交換する（CとBのプールのやり取り）というクロスエクスチェンジスワップをご提案します。

一度に2つのプールで取引を行うため、[**許容スリッページ**](slippage-tolerance.md)や[**流動性プロバイダー手数料**](fees.md)が2倍になりますので、ご注意ください。&#x20;

{% content-ref url="../how-to/use-cross-exchange.md" %}
[use-cross-exchange.md](../how-to/use-cross-exchange.md)
{% endcontent-ref %}
