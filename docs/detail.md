## APIの詳しい仕様 {#detail}

駅簡易情報API(/station/light)は、「[アプリケーションを作ってみよう](/docs/app.md)」で作成したアプリケーションの駅入力フォームの裏側で利用されている機能です。以下のURLにアクセスします。

```
https://api.ekispert.jp/v1/json/station/light?name=渋谷&type=train&key=LE_EeMdKVHwJQSen
```

{% hint %}
ブラウザでJSONのレスポンスデータを見たときに、改行が無く見づらいと感じたら、ブラウザが提供する「ブラウザ拡張機能」を利用してみてください。
本書付録の「[オススメのブラウザ拡張機能](/docs/tools.md#extension)」をご参考にしてください。

![img](/img/10.png)

<p class="caption">ブラウザでURLを開いた時の画面（JSON、ブラウザ拡張機能無し）</p>

![img](/img/use_extension.png)

<p class="caption">ブラウザでURLを開いた時の画面（JSON、ブラウザ拡張機能有り）</p>

{% endhint %}

|パラメータ|説明|
|---|---|
|name|候補文字列から駅検索を行うためのパラメータです。|
|type|駅の交通種別を指定するパラメータです。|

![img](/img/station.png)

<p class="caption">レスポンスデータの解説</p>

駅すぱあとが持つ駅には、「駅コード」[^1]と呼ばれるユニークな値が振られています。駅コードは、駅名変更などに関わらず基本的に不変ですので、保存を前提とした利用は駅コードの利用が推奨されます。「都道府県コード」[^2]とは、駅すぱあとWebサービスで定める都道府県に紐づいたコードです。


## 脚注
[^1]: 駅コード http://docs.ekispert.com/v1/le/dictionary/station-code/
[^2]: 都道府県コード http://docs.ekispert.com/v1/le/dictionary/prefecture-code/
