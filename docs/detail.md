## APIの詳しい仕様 {#detail}

### 駅簡易情報API {#station-light}

駅簡易情報API(/station/light)は、「[アプリケーションを作ってみよう](/docs/app.md)」で作成したアプリケーションの駅入力フォームの裏側で利用されている機能です。以下のURLにアクセスします。

```
https://api.ekispert.jp/v1/json/station/light?name=渋谷&type=train&key=LE_EeMdKVHwJQSen
```

{% hint %}
ブラウザでJSONのレスポンスデータを見たときに、改行が無く見づらいと感じたら、ブラウザが提供する「ブラウザ拡張機能」を利用してみてください。
本書付録の「[オススメのブラウザ拡張機能](/docs/tools.md#extension)」をご参考にしてください。


![img](https://docs.google.com/drawings/d/e/2PACX-1vTFzcm6K_fLyks2jJzbA60HYsSJKt_zKwcReRXVqMNh2uZAtFlwsmkgV-TDPazLxaRcvuD_L9Fz2dHv/pub?w=1088&h=511)

<p class="caption">ブラウザでURLを開いた時の画面（JSON、ブラウザ拡張機能無し）</p>


![img](https://docs.google.com/drawings/d/e/2PACX-1vRXAUMEJqApI7PL1CObdEHUs4n41P5YU1qm2y3X5WyT6nEEHrhp6aUcnqWWhsgY3i4WNX0OTfkSxsSi/pub?w=1084&h=663)

<p class="caption">ブラウザでURLを開いた時の画面（JSON、ブラウザ拡張機能有り）</p>

{% endhint %}

|パラメータ|説明|
|---|---|
|name|候補文字列から駅検索を行うためのパラメータです。|
|type|駅の交通種別を指定するパラメータです。|


![img](https://docs.google.com/drawings/d/e/2PACX-1vRHuxBG5ycjHcqu5tQdKn_SkBA66lOe2C6PpeD85rc8FjgRDOUyoqA1uhKVuzaW8hz5FghYWtm9baq8/pub?w=783&h=566)

<p class="caption">レスポンスデータの解説</p>

駅すぱあとが持つ駅には、「駅コード」[^1]と呼ばれるユニークな値が振られています。駅コードは、駅名変更などに関わらず基本的に不変ですので、保存を前提とした利用は駅コードの利用が推奨されます。「都道府県コード」[^2]とは、駅すぱあとWebサービスで定める都道府県に紐づいたコードです。


## 脚注
[^1]: 駅コード http://docs.ekispert.com/v1/le/dictionary/station-code/
[^2]: 都道府県コード http://docs.ekispert.com/v1/le/dictionary/prefecture-code/
