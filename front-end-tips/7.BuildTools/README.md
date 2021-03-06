# Task Runners
WebページやWebアプリを開発する時、それぞれライブラリやツールを個別にインストールして管理実行する手間を省区ために一元管理しバックグラウンドで動かす仕組みのことをタスクランナーという。
共通の設定ファイルを利用することで、チーム全員が同様の環境をすぐに構築できて、特に意識せずとも同じような処理を行えるようにする。

### HTMLやCSSをより便利に、多機能に記述するためのライブラリやツール
- EJSやpug、HAMLなどのテンプレートエンジン
HTMLをより簡略にかけたり、共通で使いまわせるレイアウトやパーツを使ったり、JSONファイルからページの量産ができる。
- SASS, PostCSSなどのCSSプリプロセッサ
CSSをより読みやすく書いたり、変数や関数などを利用できる。また、将来的に公式のCSSで採用される機能を先取りして利用することもできる。
- BabelやTypescriptなどのJavascriptトランスパイラ
より厳密なルールで型を定義したり、将来的に採用されることが決まっている仕様で記述したりできる。CoffeScriptのような、記述を簡便化することが目的のものもある。
- ReactやVue、Angularなどのフレームワーク
SPA開発などフロント面で多機能なUI実装をしたり、様々な目的を持つライブラリが非常にたくさんある。
- CommonJSやAMDなどのモジュールバンドラ
複数ファイルに分割されたJavaScriptをModuleとして扱い、ひとつのファイルに結合する。ただ順番にファイルを結合(concat)するのではなく、それらの関数や変数値などの依存関係を解決した上で1つに結びつける。
- eslintやstylelintなどの構文チェッカー
CSSやJavascriptに構文ミスが無いか検証するツール。細かく記述ルールを設定することもできる。

### Web開発をする際に開発に便利な環境を導入する
- 作成しているページをリアルタイムにスマホで確認したり、 ファイルを編集するたびに自動でリロードしてくれるローカルサーバ
- 画像を圧縮したり、CSSスプライト用の画像を自動で作成するプラグイン

## npm script
- メリット：npmの本来の機能のみでよく、シンプルな構成になる。ビルドパフォーマンスが高い
- デメリット：モジュールバンドラとしての機能は貧弱。自由度は低め、レファレンスも少ない
## webpack
- メリット：モジュールバンドらとしては人気が高く、レファレンスも多い
- デメリット：設定が難しめ、ファイル操作などは弱い



[【保存版】gulp, webpack, parcel...増え続けるタスクランナーの特徴を理解して最適なものを選択しよう](https://hira.page/blog/201712_taskrunner/)