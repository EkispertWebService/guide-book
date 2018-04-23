# APIの解説

ここまでで、駅すぱあとWebサービスを使ったアプリケーションを実装しました。では、アプリケーション内ではどんな内容のリクエストを送信し、APIからどのようなデータが返却されているのでしょうか？こちらの項目では、駅簡易情報API(/station/light)[^1]と経路探索API(/search/course/extreme)[^2]を例に、詳しく解説します。

## APIのリクエストURLを理解する {#url}

次のURLをWebブラウザでアクセスしてみてください。「アクセスキー」の部分はご自身のアクセスキーに置き換えてください。Webブラウザの画面は、図6のように表示されます。

```
https://api.ekispert.jp/v1/xml/station/light?name=渋谷&type=train&key=アクセスキー
```

▼図6 WebブラウザでURLを開いた時の画面

![img](https://docs.google.com/drawings/d/e/2PACX-1vS8UOsnDyXcou5LK_YKr3p1Cv27C6lVPJf8kiPNzdFcpwdabsbaVR0v7wSstO02H6s_aQj6La7e6imF/pub?w=928&h=532)

{% hint %}
リスト3のようなレスポンスが表示された場合は、アクセスキーが間違っている可能性があります。今一度、アクセスキーをお確かめください。

▼リスト3 403エラーのレスポンス例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ResultSet apiVersion="1.27.0.0" engineVersion="">
  <Error code="W403">
    <Message>認証エラー</Message>
  </Error>
</ResultSet>
```
{% endhint %}

何気なくアクセスしたURLは、APIのバージョン、レスポンスのデータフォーマット、APIの機能、そして、クエリパラメータで構成されています（図7）。

▼図7 APIのリクエストURL構成

![img](https://docs.google.com/drawings/d/e/2PACX-1vQsqQEht02Gg7cxKrZUVXPciadzzxb6S9VSAPdQ9Vep20VuuYgATIxt65tj7ypI1kkVx7xvJ4Sm2o-5/pub?w=1578&h=303)

## レスポンスのデータフォーマット {#format}

駅すぱあとWebサービスのレスポンスはXMLまたはJSONで取得可能です。図7の「データフォーマット」部分を「xml」と指定すればXMLが、「json」と指定すればJSONのフォーマットでデータが返ってきます。

## APIの詳しい仕様 {#detail}

### 駅簡易API {#station-light}

駅簡易情報API(/station/light)は、「[アプリケーションを作ってみよう](/docs/app.md)」で作成したアプリケーションの駅入力フォームの裏側で利用されている機能です。以下のURLにアクセスします。

```
https://api.ekispert.jp/v1/json/station/light?name=渋谷&type=train&key=アクセスキー
```

▼表1 指定されたパラメータの説明

|パラメータ|説明|
|---|---|
|name|候補文字列から駅検索を行うためのパラメータです。|
|type|駅の交通種別を指定するパラメータです。|

▼図8 レスポンスデータの解説

![img](https://docs.google.com/drawings/d/e/2PACX-1vRHuxBG5ycjHcqu5tQdKn_SkBA66lOe2C6PpeD85rc8FjgRDOUyoqA1uhKVuzaW8hz5FghYWtm9baq8/pub?w=783&h=566)

駅すぱあとが持つ駅には、「駅コード」[^3]と呼ばれるユニークな値が振られています。駅コードは、駅名変更などに関わらず基本的に不変ですので、保存を前提とした利用は駅コードの利用が推奨されます。「都道府県コード」[^4]とは、駅すぱあとWebサービスで定める都道府県に紐づいたコードです。

### 経路探索API {#search-course-extreme}

経路探索API(/search/course/extreme)は、「[アプリケーションを作ってみよう](/docs/app.md)」で作成したアプリケーションの探索ボタンの裏側で利用されている機能です。以下のURLにアクセスしてみてください。

```
https://api.ekispert.jp/v1/json/search/course/extreme?viaList=22741:22715&searchType=plain&key=アクセスキー
```

▼表2 指定されたパラメータの説明

|パラメータ|説明|
|---|---|
|viaList|出発地、経由地、到着地を指定するパラメータです。それぞれをカンマ「:」で区切ります。「22741」は新宿駅の駅コード、「22715」は渋谷駅の駅コードを表しています。viaListには、駅コード以外にも、駅の名称、緯度経度、住所などを指定することができます。|
|searchType|探索種別[^5]を指定するパラメータです。駅すぱあとWebサービスでは、ダイヤデータを使う探索（ダイヤによる探索[^6]）と、平日日中の平均的な所要時間を利用した探索（平均待ち時間による探索[^7]）の二つの探索方法があり、それをさらに細分化したものが探索種別となります。|

レスポンスには、新宿駅から渋谷駅までの、平均待ち時間による探索での経路探索結果が返ってきます。アプリケーションでどのようにレスポンスデータが使われているのか、いくつかピックアップして解説します。

所要時間の値は、`timeOther`、`timeOnBoard`、`timeWalk`の合計で求まります（図9）。

▼図9 レスポンスデータの解説 所要時間

![img](https://docs.google.com/drawings/d/e/2PACX-1vTwB3eJ_QBoXI_nx-VVnMF2oR3rqfTXZYTbLa93MfBh8Nil3f-mByu8280rn9Nfmaal5jcHrNRBkz-W/pub?w=846&h=416)

経路全体の運賃は、`kind`の値が`FareSummary`となっている`Oneway`の値です。経路の一区間の運賃は、`kind`の値が`Fare`となっている`Oneway`の値です（図10）。

▼図10 レスポンスデータの解説 運賃

![img](https://docs.google.com/drawings/d/e/2PACX-1vS_kwOKH6Tr053FD2lDzu9jznundjbIn0vSjodlV6W1M3Zvgdn7BVhjz49JxgqAUNOFYtWLc9Gu9Hy6/pub?w=892&h=411)

`Point[0].Station.Name`、`Line.Name、Point[1].Station.Name`を交互に並べることで、経路を表現できます（図11）。

▼図11 レスポンスデータの解説 経路表現

![img](https://docs.google.com/drawings/d/e/2PACX-1vRdrHjugJSU_7M8623Pizm95OYL8yjK9YPvIPbJwDzpZUiAQrj7u58hpLnFV8Pv2P5Ryj90E8bkOiaP/pub?w=1038&h=619)


## 脚注
[^1]: 駅簡易情報API http://docs.ekispert.com/v1/api/station/light.html
[^2]: 経路探索API http://docs.ekispert.com/v1/api/search/course/extreme.html
[^3]: 駅コード http://docs.ekispert.com/v1/dictionary/station-code/
[^4]: 都道府県コード http://docs.ekispert.com/v1/dictionary/prefecture-code/
[^5]: 探索種別 http://docs.ekispert.com/v1/dictionary/search-type/
[^6]: ダイヤによる探索 http://docs.ekispert.com/v1/dictionary/search-course-by-diagram/
[^7]: 平均待ち時間による探索 http://docs.ekispert.com/v1/dictionary/search-course-by-average-time/
