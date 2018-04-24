# アプリケーションを作ってみよう

それでは、ここからは簡単なWebアプリケーションを例に実際の開発の流れを見て行きましょう。一緒に手を動かしながら読み進めていただくと、より理解が深まります。

入力された文字列から駅を確定し、経路探索を行い結果を表示する簡単なWebアプリケーションを作ります。

▼図1 実装するアプリケーション画面イメージ

![img1](https://docs.google.com/drawings/d/e/2PACX-1vQEwohVNihVrcpstBEzVi1lXT_rjA_MybKX-3sSK-R2FBz1kklEppFinA5zA2rYx_QU8Ebzq5xunqG5/pub?w=1240&h=884)


駅すぱあとWebサービスには、無料で使える「フリープラン」と、全ての機能が使える「スタンダードプラン」[^1]の2つのプランがあります。
今回はスタンダードプランで使える機能でアプリケーションを作っていくので、スタンダードプランが90日間無料で利用できる評価版の申し込み[^2]を行います。
数営業日後に、登録したメールアドレス宛てにアクセスキーが届きます。

アクセスキーが取得できたところで、早速実装に移ります。最初から実装するのも良いですが、ここでは「HTML5インターフェースサンプル」[^3]を使い、シンプルでかつ簡単に実装していきます。HTML5インターフェースサンプルとは、HTMLとJavaScript、CSSで実装された画面をサンプルとして提供しているものです。
また、本書では、Webアプリケーションをサクッと動かすのに便利なツール「JSFiddle」[^4]を使って説明していきます。会員登録不要で、ブラウザ上でHTML、JavaScriptコードを実行し、動作確認ができます。JSFiddleにアクセスすると、画面上に4つの枠が表示されます。左上がHTML、左下がJavaScript、右上がCSS、そして右下にそれらを組み合わせた結果が表示されます（図2）。

▼図2 JSFiddleの画面

![img2](https://docs.google.com/drawings/d/e/2PACX-1vSuw02x_PKsm_w6BSAp7rNB4qLTY-jwtNNFwJlqIm_-yGgq_VhFl9Nz38BMV4CBLeYZn6eZStVmZfpR/pub?w=1392&h=868)


HTML、JavaScriptをリスト1、リスト2のように入力します。JavaScriptに関しては、コード例の中にアクセスキーを入力する箇所があります。

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

▼リスト2 JavaScriptソースコード

```JavaScript
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

次に、HTML5インターフェースサンプルを読み込みます。JSFiddleの画面左に「Resources」と書かれた項目があります。

▼図3 JSFiddleの画面左項目

![img](https://docs.google.com/drawings/d/e/2PACX-1vTNdrHorO7Jl_u2fUFM0isId5UoK5K-1FCD3HIiPIlsbVYprNvcavQ-Czv6b2vwjkLLWmTU9NqOtxdd/pub?w=212&h=349)

「Resources」をクリックすると、URL入力欄が出てきます。以下の4つのURLを一つずつ入力欄に入力し、「+」ボタンを押して確定させます。

```
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiStation/expCss/expGuiStation.css
```

```
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiCourse/expCss/expGuiCourse.css
```

```
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiStation/expGuiStation.js
```

```
https://rawgit.com/EkispertWebService/GUI/ed686b/expGuiCourse/expGuiCourse.js
```

▼図4 「Resources」にURLを入力している様子

![img](https://docs.google.com/drawings/d/e/2PACX-1vSNJBlbFF0q5zSlY3rCLt-qWt9MfjmtrxG80klOh71UW--FDv1bw5bWUc-Bbs57TrExLey6DmSJKNGs/pub?w=209&h=311)

▼図5 URLの設定が全て完了した状態

![img](https://docs.google.com/drawings/d/e/2PACX-1vQ2tUPOIbWxOXM21bqRc3Bb3ciRGjZoztu10CANE10lZeDpLADcKZB5A3qP-60DPKs7fEYoaZGTNKCe/pub?w=213&h=391)

これで設定が完了しました。「Run」をクリックし、ソースコードを実行すると、画面右下に実行結果が表示されます。

▼図6 「Run」を実行した状態

![img](https://docs.google.com/drawings/d/e/2PACX-1vR4_IiJPjADK4v6_mMvlOdm7yLJguYWS4aRsNfwL8gy0uu0S6IXrbA9QVFETApoJ2BI02R_wSwZTn5h/pub?w=1044&h=621)

駅が検索でき、経路探索結果が表示されるアプリケーションの実装ができます。

▼図7 アプリケーション実行結果

![img](https://docs.google.com/drawings/d/e/2PACX-1vTYE4DXFueLrsS-2ceyci4Fbgif59CLUS1Y4mDkxAV0mq8wcuS75vpffjwOd4uK0NhGr42dK9XoVDxz/pub?w=820&h=569)

{% hint %}
アプリケーションが図7のような挙動にならなかったら、ブラウザが提供する「開発者ツール」を使ってデバッグしましょう。「開発者ツール」と聞いてピンとこない方は、本書付録の「[開発者ツールを使いこなす](/docs/appendix.md#devtool)」をご参考にしてください。
{% endhint %}


## 脚注
[^1]: スタンダードプランは法人のお客様のみご利用いただけます。
[^2]: スタンダードプラン評価版申し込みページ https://ekiworld.net/trial/index.php?case=6
[^3]: HTML5インターフェースサンプル https://github.com/EkispertWebService/GUI
[^4]: JSFiddle https://jsfiddle.net/
