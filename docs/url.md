## APIのリクエストURLを理解する {#url}

次のURLをブラウザでアクセスしてみてください。

```
https://api.ekispert.jp/v1/xml/station/light?name=渋谷&type=train&key=LE_EeMdKVHwJQSen
```

![img](https://docs.google.com/drawings/d/e/2PACX-1vS8UOsnDyXcou5LK_YKr3p1Cv27C6lVPJf8kiPNzdFcpwdabsbaVR0v7wSstO02H6s_aQj6La7e6imF/pub?w=928&h=532)

<p class="caption">ブラウザでURLを開いた時の画面（XML）</p>

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

何気なくアクセスしたURLは、APIのバージョン、レスポンスのデータフォーマット、APIの機能、そして、クエリパラメータで構成されています。

![img](https://docs.google.com/drawings/d/e/2PACX-1vQsqQEht02Gg7cxKrZUVXPciadzzxb6S9VSAPdQ9Vep20VuuYgATIxt65tj7ypI1kkVx7xvJ4Sm2o-5/pub?w=1578&h=303)

<p class="caption">APIのリクエストURL構成</p>
