### 開発者ツールを使いこなす {#devtool}

今回実装したアプリケーションのように、JavaScriptを使ってブラウザ上で動くアプリケーションを作るなら、「開発者ツール」を使いこなしましょう。開発速度がグッとあがるはずです。
開発者ツールとは、ブラウザに搭載されているデバッグツールです。「デベロッパーツール」とも呼ばれることがありますが、本書では「開発者ツール」と表記します。
現在だとほぼ全てのブラウザで標準搭載されており、Windowsの場合は「F12」、Macの場合は「Option + Command + i」で起動できます。


![img](https://docs.google.com/drawings/d/e/2PACX-1vRTrdKd8-r3fvmruik_zVFc7Royuy5M5wUz9HCGVnv2V7hpOXIhWtbLIurgQXshe__pp5v6LKe3B2n8/pub?w=928&h=519)

<p class="caption">ブラウザ上で開発者ツールを立ち上げた状態（Google Chrome）</p>

ここからは、Google Chromeを例に説明します。

開発者ツールの「Console」パネルは、JavaScriptのデバッグに役立ちます。
アプリケーションが意図しない挙動をしている時は、まずConsoleパネルでエラーが発生していないか確認しましょう。


![img](https://docs.google.com/drawings/d/e/2PACX-1vRMR0ttL9ELmA86zNNYdaQwhLDdNzxv1C0BOr7d6NqyX4wDxMnihifaH-H6Hpequ6aSdkjABVClztEC/pub?w=928&h=518)

<p class="caption">開発者ツールのConsoleパネル（Javascriptコード内でシンタックスエラーが発生している場面）</p>

「Network」パネルは、表示しているページで行うHTTP通信が一覧として現れ、リクエスト、レスポンスの内容やアクセスの状況を見ることができます。つまり、駅すぱあとWebサービスへのアクセスに成功しているか、どんなやりとりがされているか確認できます。


![img](https://docs.google.com/drawings/d/e/2PACX-1vQCO1XSe_pKfQXCIKEbHAw3jlSm1BEBXfB8reMIVPjmp4AO2C-m3JwKNzR6eYRDJXer-lAXBhKdzyBb/pub?w=928&h=514)

<p class="caption">開発者ツールのNetworkパネル</p>

詳細な使い方に関してもっと知りたくなったかと思いますが、インターネット上にたくさんの情報が公開されているので、ここでは割愛します。
興味を持って探求することはエンジニアとしてのスキルアップに繋がるはずです。ぜひ調べてみてください。
