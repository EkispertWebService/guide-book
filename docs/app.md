# アプリケーションを作ってみよう

それでは、ここからは簡単なWebアプリケーションを例に実際の開発の流れを見て行きましょう。一緒に手を動かしながら読み進めていただくと、より理解が深まります。

入力された文字列から駅を確定し、経路探索を行い結果を表示する簡単なWebアプリケーションを作ります。

![img](/img/1.png)

<p class="caption">実装するアプリケーション画面イメージ</p>

駅すぱあとWebサービスには、無料で使える「フリープラン」[^1]と、全ての機能が使える「スタンダードプラン」[^2]の2つのプランがあります。
今回はフリープランで使える機能を用いてアプリケーションを作成します。

駅すぱあとWebサービスをご利用いただくにはアクセスキー[^3]が必要ですが、本書をお読みいただいている皆さまがその場で試していただけるようにアクセスキーを用意しました。

書籍限定 お試し用アクセスキー：**LE_EeMdKVHwJQSen**  
※ フリープランの機能をお試しいただけるアクセスキーです。

では早速実装にうつります。

`index.html`など、適当なファイルを作成し、HTMLをリスト1のように入力します。

Webアプリケーションをサクッと動かすのに便利なツール「JS Bin」[^4]、「JSFiddle」[^5]などをご利用いただくのも手です。

▼リスト1 HTMLソースコード

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>駅すぱあとWebサービス 経路探索サンプルアプリ</title>
  <script src="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiStation/expGuiStation.js"></script>
  <script src="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiCourseLight/expGuiCourseLight.js"></script>
  <link rel="stylesheet" href="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiStation/expCss/expGuiStation.css" />
</head>
<script>
var accessKey = "LE_EeMdKVHwJQSen"; // お試し用のアクセスキー
var depStationApp;
var arrStationApp;
var courseLight;

function init() {
  depStationApp = new expGuiStation(document.getElementById("depStation"));
  depStationApp.setConfigure("key", accessKey);
  depStationApp.setConfigure("ssl", true);
  depStationApp.dispStation();

  arrStationApp = new expGuiStation(document.getElementById("arrStation"));
  arrStationApp.setConfigure("key", accessKey);
  arrStationApp.setConfigure("ssl", true);
  arrStationApp.dispStation();

  courseLight = new expGuiCourseLight();
  courseLight.setConfigure("key", accessKey);
  courseLight.setConfigure("ssl", true);
}

// 探索ボタンの動作
window.onload = function() {
  var search = document.getElementById('search');
  search.addEventListener('click', (e) => {

    // 候補を閉じる
    depStationApp.closeStationList();
    arrStationApp.closeStationList();

    var searchObj = courseLight.createSearchInterface();

    // 出発着の設定
    searchObj.setFrom(depStationApp.getStationCode());
    searchObj.setTo(arrStationApp.getStationCode());

    // 探索を実行
    courseLight.search(searchObj, function(isSuccess) {
      if (!isSuccess) {
        alert("探索結果が取得できませんでした");
      } else {
        document.getElementById("ekispertUrl").textContent = "駅すぱあと for web の探索結果を表示する";
        document.getElementById("ekispertUrl").href = courseLight.getResourceURI();
      }
    });
  })
};

window.addEventListener('load', init);

</script>
<body>
<div>
  出発地
  <div id="depStation"></div>
</div>
<div>
  目的地
  <div id="arrStation"></div>
</div>
<button id="search">探索</button>
<a id="ekispertUrl" href="" target="_blank"></a>
</body>
</html>
```

コードの中身を見ると、
`<script src="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiStation/expGuiStation.js"></script>`など、いくつかの外部ファイルをインクルードしていますが、これは「HTML5インターフェースサンプル」[^6]です。
HTML5インターフェースサンプルとは、HTMLとJavaScript、CSSで実装された画面をサンプルとして提供しているものです。

ファイルに入力し終えたら、ファイルをブラウザで開いてください。
駅が検索でき、経路探索結果のURLが表示されるアプリケーションができました。

![img](/img/result.png)

<p class="caption">アプリケーション実行結果</p>

{% hint %}
アプリケーションが意図した挙動にならなかったら、ブラウザが提供する「開発者ツール」を使ってデバッグしましょう。
「開発者ツール」と聞いてピンとこない方は、本書付録の「[開発者ツールを使いこなす](/docs/devtool.md)」をご参考にしてください。
{% endhint %}


## 脚注
[^1]: 駅すぱあとWebサービス フリープラン https://ekiworld.net/service/lp/webservice/
[^2]: 駅すぱあとWebサービス スタンダードプラン https://ekiworld.net/service/sier/webservice/index.html <br>※ スタンダードプランは法人のお客様のみご利用いただけます。
[^3]: Webから申し込みいただくことで、アクセスキーを取得できます。 <br>フリープラン: https://ekiworld.net/free_provision/index.php <br>スタンダードプラン: https://ekiworld.net/trial/index.php?case=6
[^4]: JS Bin https://jsbin.com/
[^5]: JSFiddle https://jsfiddle.net/
[^6]: HTML5インターフェースサンプル https://github.com/EkispertWebService/GUI
