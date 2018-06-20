## APIのリクエストURLを理解する {#url}

次のURLをブラウザでアクセスしてみてください。

```
https://api.ekispert.jp/v1/xml/station/light?name=渋谷&type=train&key=LE_EeMdKVHwJQSen
```
![img](/img/8.png)

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

![img](/img/9.png)

<p class="caption">APIのリクエストURL構成</p>
