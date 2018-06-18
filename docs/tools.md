## 開発お役立ちツール {#tools}

駅すぱあとWebサービスを使って開発をする上で、実際に著者が活用しているツールをご紹介します。

### APIの仕様理解を深める「API Checker」 {#apichecker}

駅すぱあとWebサービスのドキュメントサイトでは、APIを試すのにぴったりなツール「API Chercker」[^1]を用意しています。これは、APIの仕様を調べるだけではなく、APIをインタラクティブに呼び出し挙動を試すことができるため、APIの理解を深めることができます。


![img](https://docs.google.com/drawings/d/e/2PACX-1vQInUlCEyqmk2MGZdXlTL1nO2tNRJynxbxMV9ZdZJvpx9BJISZ4m9KBkzw9Fzr2cpVMvv3cw0SD2d0X/pub?w=1394&h=755)

<p class="caption">ドキュメントサイトで用意しているAPI Checkerの画面</p>

### オススメのブラウザ拡張機能 {#extension}

「ブラウザ拡張機能」とは、ブラウザの機能を拡張するためのプログラムです。
「プラグイン」とも呼ばれることがありますが、本書では「ブラウザ拡張機能」と表記します。

ブラウザ拡張機能のインストール方法や管理方法は割愛し、WebAPIを使って開発する上で便利なGoogle Chromeのブラウザ拡張機能を紹介します。
ここでは、Google Chromeのブラウザ拡張機能を紹介しますが、他のブラウザでも類似するブラウザ拡張機能を提供していると思いますので、探してみてください。

##### ・JSON Formatter

![img](https://docs.google.com/drawings/d/e/2PACX-1vQ_pl6qjpU3-wIgHIfXGP6DtXkfPDZ77Nvf5qBVbYkbiojxPHZaFyLv0CtTNCA68ysGNO2KUCOkklDE/pub?w=789&h=330)

JSONデータがブラウザで見やすくなるブラウザ拡張機能です。WebAPIのレスポンスをブラウザで確認する時に活用します。

https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa

##### ・XML Tree

![img](https://docs.google.com/drawings/d/e/2PACX-1vR4u3ZtwyhrVZE_ox8kYhMwDa-Yy5nLk-Vr1POJBSA95GrAHRwdYQfJuc6iwSFQpq7eFf5mqEahWJDI/pub?w=913&h=411)

XMLデータがブラウザで見やすくなるブラウザ拡張機能です。さらに、XPathでXMLデータからデータを抽出することもできます。

https://chrome.google.com/webstore/detail/xml-tree/gbammbheopgpmaagmckhpjbfgdfkpadb

##### ・ウェブページ全体をスクリーンショット - FireShot

ページ全体をスクリーンショット出来るブラウザ拡張機能です。
実装するアプリケーションのレビューなどで活用できます。

https://chrome.google.com/webstore/detail/take-webpage-screenshots/mcbpblocgmgfnpjjppndjkmgjaogfceg

### 開発者ツールを使いこなす {#devtool}

今回実装したアプリケーションのように、JavaScriptを使ってブラウザ上で動くアプリケーションを作るなら、「開発者ツール」を使いこなしましょう。開発速度がグッとあがるはずです。
開発者ツールとは、ブラウザに搭載されているデバッグツールです。「デベロッパーツール」とも呼ばれることがありますが、本書では「開発者ツール」と表記します。現在だとほぼ全てのブラウザで標準搭載されており、Windowsの場合は「F12」、Macの場合は「Option + Command + i」で起動できます。


![img](https://docs.google.com/drawings/d/e/2PACX-1vRA6DSbkgyWfi_PjDghsvjZhXnU49zA77V3vZR16esp1zrz8xrFrQRRTgINHmwoNXJC6Srr5liWhmR0/pub?w=1393&h=784)

<p class="caption">ブラウザ上で開発者ツールを立ち上げた状態（Google Chrome）</p>

ここからは、Google Chromeを例に説明します。開発者ツールの「Console」パネルは、JavaScriptのデバッグに役立ちます。アプリケーションが意図しない挙動をしている時は、まずConsoleパネルでエラーが発生していないか確認しましょう。


![img](https://docs.google.com/drawings/d/e/2PACX-1vTXGa1E75cNr9On3Q-03Paf9JlUomwx3ta1pzSda0uIBVOtwIrdZS-qtmB7EjA1RHpdsxlMr95pi7wI/pub?w=1392&h=641)

<p class="caption">開発者ツールのConsoleパネル（Javascriptコード内でシンタックスエラーが発生している場面）</p>

「Network」パネルは、表示しているページで行うHTTP通信が一覧として現れ、リクエスト、レスポンスの内容やアクセスの状況を見ることができます。つまり、駅すぱあとWebサービスへのアクセスに成功しているか、どんなやりとりがされているか確認できます。


![img](https://docs.google.com/drawings/d/e/2PACX-1vSAYbY59MLD_lIQdp3cb1BJ7KQuVXBvjSIKes-Uz0OUJ4h08SWc4ohiC__1eBZgoHRqKGZwdhJ6BGgy/pub?w=1393&h=660)

<p class="caption">開発者ツールのNetworkパネル</p>

詳細な使い方に関してもっと知りたくなったかと思いますが、インターネット上にたくさんの情報が公開されているので、ここでは割愛します。
興味を持って探求することはエンジニアとしてのスキルアップに繋がるはずです。ぜひ調べてみてください。

## 脚注

[^1]: API Checker <br>スタンダードプラン: http://docs.ekispert.com/v1/tools/api-checker/<br>フリープラン: http://docs.ekispert.com/v1/le/tools/api-checker/
