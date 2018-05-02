## APIの詳しい仕様 {#detail}

### 駅簡易情報API {#station-light}

駅簡易情報API(/station/light)は、「[アプリケーションを作ってみよう](/docs/app.md)」で作成したアプリケーションの駅入力フォームの裏側で利用されている機能です。以下のURLにアクセスします。

```
https://api.ekispert.jp/v1/json/station/light?name=渋谷&type=train&key=アクセスキー
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

### 経路探索API {#search-course-extreme}

経路探索API(/search/course/extreme)は、「[アプリケーションを作ってみよう](/docs/app.md)」で作成したアプリケーションの探索ボタンの裏側で利用されている機能です。以下のURLにアクセスしてみてください。

```
https://api.ekispert.jp/v1/json/search/course/extreme?viaList=22741:22715&searchType=plain&key=アクセスキー
```

|パラメータ|説明|
|---|---|
|viaList|出発地、経由地、到着地を指定するパラメータです。それぞれをカンマ「:」で区切ります。「22741」は新宿駅の駅コード、「22715」は渋谷駅の駅コードを表しています。viaListには、駅コード以外にも、駅の名称、緯度経度、住所などを指定することができます。|
|searchType|探索種別[^3]を指定するパラメータです。駅すぱあとWebサービスでは、ダイヤデータを使う探索（ダイヤによる探索[^4]）と、平日日中の平均的な所要時間を利用した探索（平均待ち時間による探索[^5]）の二つの探索方法があり、それをさらに細分化したものが探索種別となります。|

レスポンスには、新宿駅から渋谷駅までの、平均待ち時間による探索での経路探索結果が返ってきます。アプリケーションでどのようにレスポンスデータが使われているのか、いくつかピックアップして解説します。

所要時間の値は、`timeOther`、`timeOnBoard`、`timeWalk`の合計で求まります。


![img](https://docs.google.com/drawings/d/e/2PACX-1vTwB3eJ_QBoXI_nx-VVnMF2oR3rqfTXZYTbLa93MfBh8Nil3f-mByu8280rn9Nfmaal5jcHrNRBkz-W/pub?w=846&h=416)

<p class="caption">レスポンスデータの解説 所要時間</p>

経路全体の運賃は、`kind`の値が`FareSummary`となっている`Oneway`の値です。経路の一区間の運賃は、`kind`の値が`Fare`となっている`Oneway`の値です。


![img](https://docs.google.com/drawings/d/e/2PACX-1vS_kwOKH6Tr053FD2lDzu9jznundjbIn0vSjodlV6W1M3Zvgdn7BVhjz49JxgqAUNOFYtWLc9Gu9Hy6/pub?w=892&h=411)

<p class="caption">レスポンスデータの解説 運賃</p>

`Point[0].Station.Name`、`Line.Name、Point[1].Station.Name`を交互に並べることで、経路を表現できます。


![img](https://docs.google.com/drawings/d/e/2PACX-1vRdrHjugJSU_7M8623Pizm95OYL8yjK9YPvIPbJwDzpZUiAQrj7u58hpLnFV8Pv2P5Ryj90E8bkOiaP/pub?w=1038&h=619)

<p class="caption">レスポンスデータの解説 経路表現</p>


## 脚注
[^1]: 駅コード http://docs.ekispert.com/v1/dictionary/station-code/
[^2]: 都道府県コード http://docs.ekispert.com/v1/dictionary/prefecture-code/
[^3]: 探索種別 http://docs.ekispert.com/v1/dictionary/search-type/
[^4]: ダイヤによる探索 http://docs.ekispert.com/v1/dictionary/search-course-by-diagram/
[^5]: 平均待ち時間による探索 http://docs.ekispert.com/v1/dictionary/search-course-by-average-time/
