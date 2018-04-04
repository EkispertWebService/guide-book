# アプリケーションを作ってみよう

それでは、ここからは簡単なWebアプリケーションを例に実際の開発の流れを見て行きましょう。時間があれば一緒に手を動かしながら読み進めていただくと、より理解が深まります。

入力された文字列から駅を確定し、経路探索を行い結果を表示する簡単なWebアプリケーションを組んでいきます。

▼図1 実装するアプリケーション画面イメージ

![img](/img/1.png)

駅すぱあとWebサービスには、無料で使えるフリープランと、全ての機能が使えるスタンダードプランの2つのプランがあります。
今回はスタンダードプランで使える機能でアプリケーションを作っていくので、スタンダードプランが90日間無料で利用できる評価版の申し込み[^1]を行います。
数営業日後に、登録したメールアドレス宛てにアクセスキーが届きます。

アクセスキーが取得できたところで、早速実装に移ります。最初から実装するのも良いですが、ここでは「HTML5インターフェースサンプル」[^2]を使い、シンプルでかつ簡単に実装していきます。HTML5インターフェースサンプルとは、HTMLとJavascript、CSSで実装された画面をサンプルとして提供しているものです。
また、本資料では、Webアプリケーションをサクッと動かすのに便利なツール「JSFiddle」[^3]を使って説明していきます。会員登録不要で、Webブラウザ上でHTML、Javascriptコードを実行し、動作確認ができます。JSFiddleにアクセスすると、画面上に4つの枠が表示されます。左上がHTML、左下がJavascript、右上がCSS、そして右下にそれらを組み合わせた結果が表示されます（図2）。

▼図2 JSFiddleの画面

![img](/img/2.png)

HTML、Javascriptをリスト1、リスト2のように入力します。Javascriptに関しては、コード例の中にアクセスキーを入力する箇所があります。

▼リスト1 HTMLソースコード

```html
<div>
  出発地
  <div id="depStation"></div>
</div>
<div>
  目的地
  <div id="arrStation"></div>
</div>
<button id="search">探索</button>
<div id="result"></div>
```

▼リスト2 Javascriptソースコード

```javascript
var accessKey = "アクセスキー"; // 自身が所有するアクセスキーに書き換えてください。
var depStationApp; // 駅名入力パーツ#出発
var arrStationApp; // 駅名入力パーツ#到着
var resultApp; //経路結果表示パーツ

// 駅名入力パーツ#出発 初期化
depStationApp = new expGuiStation(document.getElementById("depStation"));
depStationApp.setConfigure("key", accessKey);
depStationApp.setConfigure("ssl", true);
depStationApp.dispStation();

// 駅名入力パーツ#到着 初期化
arrStationApp = new expGuiStation(document.getElementById("arrStation"));
arrStationApp.setConfigure("key", accessKey);
arrStationApp.setConfigure("ssl", true);
arrStationApp.dispStation();

// 経路表示パーツ初期化
resultApp = new expGuiCourse(document.getElementById("result"));
resultApp.setConfigure("key", accessKey);
resultApp.setConfigure("ssl", true);

// 探索ボタンの動作
var search = document.getElementById('search');
search.addEventListener('click', (e) => {

  // 候補を閉じる
  depStationApp.closeStationList();
  arrStationApp.closeStationList();

  var searchObject = resultApp.createSearchInterface();

  // 探索種別の設定
  searchObject.setSearchType('plain');

  // 出発着の設定
  searchObject.setViaList(depStationApp.getStationCode() + ":" + arrStationApp.getStationCode());

  // 探索を実行
  resultApp.search(searchObject, function(isSuccess) {
    if (!isSuccess) {
      alert("探索結果が取得できませんでした");
    }
  });
})
```

次に、HTML5インターフェースサンプルを読み込みます。JSFiddleの画面左に「Resources」というボタン（図3）がありますので、それをクリックするとインクルードするURLを入力する項目が出てきます。4つのURLを入力してください。

```
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiStation/expCss/expGuiStation.css
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiCourse/expCss/expGuiCourse.css
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiStation/expGuiStation.js
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiCourse/expGuiCourse.js
```

▼図3 「Resources」ボタン

![img](/img/3.png)

これで設定が完了しました。「Run」をクリックし、ソースコードを実行すると、画面右下に実行結果が表示されます。

▼図4 「Run」を実行した状態

![img](/img/4.png)

駅が検索できて、経路探索結果が表示されるアプリケーションが実装できているかと思います。

▼図5 アプリケーション実行結果

![img](/img/5.png)

{% hint %}
アプリケーションが図5のような挙動にならなかったら、Webブラウザが提供する「開発者ツール」を使ってデバッグしてみてください。「開発者ツール」と聞いてピンとこない方は、本資料付録の[開発者ツールを使いこなす](/docs/appendix.md#devtool)をご参考にしてください。
{% endhint %}


### 脚注
[^1]: スタンダードプラン評価版申し込みページ https://ekiworld.net/trial/index.php?case=6
[^2]: HTML5インターフェースサンプル https://github.com/EkispertWebService/GUI
[^3]: JSFiddle https://jsfiddle.net/
