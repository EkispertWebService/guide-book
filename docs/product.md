# What's Ekispert Web Service?

Ekispert Web Service is one of Ekispert's offer form.
We provide it that we have offered in Ekispert SDK[^1] and Ekispert Intranet[^2] as Ekispert feature.

* Route search
* Station data
* Rail data
* Corporation data
* Calculation of fare
* Train shedule
* Rail map
* Rail service information



## footnote

[^1]: Ekispert SDK https://ekiworld.net/service/sier/sdk/index.html
[^2]: Ekispert Intranet https://ekiworld.net/service/sier/intranet/index.html
[^3]: Ekispert Web Service Free Plan https://ekiworld.net/service/lp/webservice/
[^4]: Ekispert Web Service Document http://docs.ekispert.com/v1/
[^5]: HTML5 Interface Sample https://github.com/EkispertWebService/GUI






「駅すぱあとWebサービス」とは、駅すぱあとの提供形態の１つです。これまでSDK[^1]やイントラネット[^2]などで提供してきた駅すぱあとの機能をWebAPIとして提供しています。
WebAPIとして提供することで、自身の環境でのインストールや環境構築、データの更新やスケールなど従来の様々な付帯作業を気にする必要がなくなります。

様々なサービスがみなさんの価値ある仕事に集中するために用意されているように、駅すぱあとWebサービスも極力「必要だけれども差別化要因にはならないこと」を無くすよう作られています。

また、実際にコードを書くエンジニアの方に使いやすいサービスであるべく、法人向けの有償プランだけではなく個人で無料で使えるプラン[^3]を用意したり、APIのドキュメント[^4]をWebで一般公開したり、サンプルコード[^5]をGithubで公開したりしています。我々の会社のプロダクトのバックエンドとして利用されることも多く、内外での実績に支えられています。
少し技術的な話をすると、各APIはREST(Representational State Transfer)ベースで提供されており、XMLまたはJSONでの結果取得が可能です。HTTPが利用可能な言語であれば特別なライブラリ等を使わずに実装が可能です。

ちなみに機能にはどういったものがあるのでしょうか？ドキュメントを元に列挙してみました。

* 探索
* 駅の情報
* 路線の情報
* 会社の情報
* 運賃計算操作
* 時刻表
* 路線図
* 鉄道運行情報

これは抜粋ですが、さらにこのカテゴリ以下に様々なAPIがありその数は40を超えます。すべての機能を駆使すれば、iOS/Androidで提供されているような乗り換えのためのアプリを作成することだって可能です。次項からは、そのための準備を含めて解説していきます。
