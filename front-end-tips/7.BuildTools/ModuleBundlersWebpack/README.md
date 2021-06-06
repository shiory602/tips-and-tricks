# Module Bundlers
> モジュールバンドラーは、モジュールをひとまとめにする(bundle)ツール
> モジュールというのはフロントエンドの開発においては「関数」や「コンポーネント」といった機能ごとに分けたファイル
> JavaScriptの依存関係を解決し、それらを含んだ１つのファイルにまとめてくれる。
> 代表格の１つにwebpackがある。

### 用途
- JavaScriptファイルを連結する
- JavaScriptでモジュールおインポートをする
- パッケージマネージャーをnpmで一本化する
- node.jsのモジュールをブラウザ上で使う

## モジュールを１つにまとめる必要性
ブラウザ／サーバー間での通信プロトコルであるHTTP/1.1の仕組みに起因。
HTTP/1.1では一度に処理できるリクエストの数が限られているためJSのリクエストをなるべく一つにまとめてリクエストの回数を減らすことが表示速度（パフォーマンス）の観点で優れている。

基本的には一つの処理や機能（関数、コンポーネント）を一つのファイルに書いて他のファイルの中でそのモジュールが必要であればその都度読みこんで利用するというのが基本となる。

# Webpack
モジュールバンドラーツールのことで、Node.jsというJavaScript環境で使われる

## Webpackを使うメリット
- 依存関係のあるJavaScriptのモジュールを解決（静的ファイルを生成する）
- 読み込み順を気にせず、1回のリクエストで済むため効率的（通信回数が減るのでサーバーの負担も減る）
- JavaScriptモジュールをブラウザで扱える形に簡単に変換できる（最新コードで書いたものを古いブラウザにも適応するので開発効率UP）
- ローダやプラグインなどが豊富
- 様々なフレームワークで採用されているのでライブラリからサンプルを見つけやすい

## Webpackのインストール方法
### インストールの流れ
1. コマンドラインでディレクトリを作成。
```
mkdir ディレクトリ名
```
2. 作成したディレクトリ名に移動してpackage.jsonを作成。
```
npm init -y
```
3. npm経由でWebpackとwebpack-cliをインストール。
```
npm install -D webpack webpack-cli
```
### Webpackファイルを設定
4. webpack.config.jsに下記のコードを記述。
```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```
### 2つのモジュールをバンドルする手順
5. バンドルする際は、呼び出したいモジュールをインポート。
```
//モジュール1とモジュール2をimportで呼び出し
import module1 from './modules/module1';
import module2 from './modules/module2';

//変数を定義
var module1 = "Module1+";
var module2 = "Module2";

//関数に変数を投入
var returnedModule1 = module1(module1);
var returnedModule2 = module2(module2);

//結果をまとめて表示
var outputWords = returnedModule1 + returnedModule2;

console.log(outputWords);
```
6. “Module1+Module2”と出力されれば、バンドルは成功。

### CSSファイルのバンドル
7. CSSファイルのバンドルにはcss-loaderとstyle-loaderが必要。(この2つはnpmでインストール)
```
$ npm install css-loader style-loader -D
```
8. 下記のように、webpack.config.jsに追記。
```
module: {
  rules: {
    {
      test: /\.css$/,
      exclude: /node_modules/,
      use: [
        'style-loader',
        {
          loader: 'css-loader',
          options: {
            url: false,
          },
        },
      ],
    },
  },
}
```
9. 下記のように記述することで、CSSファイルをインポートする。
```
import 'style.css';
```　

## Webpackの基本要素
- Entry: エントリーポイント
JavaScriptをバンドルする上で、どのファイルを基準として依存関係を解決するかを指定する
エントリーには複数のファイルを指定することができ、エントリーポイントを指定すると、webpackはエントリーポイントで指定したファイルが依存する他のモジュールとライブラリを読み込んでくれる
- Output: アウトプット
webpackがまとめたファイルを「どこ」に「どのような名前」で出力するかを指定する
- Loader: ローダー
webpack自体はJavaScriptしか理解できないが、ローダーを使用することでJavaScript以外のCSSやHTMLといったファイルをおジュールに変換して処理を行える
設定ファイルには「ファイル名」と「適用する処理内容」を記述する
- Plugins: プラグイン
ファイルをまとめる以外のタスク（カスタムタスク）の実行ができる
プラグインは「バンドルしたJavaScriptファイルの最小化」から先に挙げたwebpackの利用例で挙げた様々な処理まで幅広く使用される


[Webpackとは？メリットや使い方、インストール方法を初心者向けに解説](https://udemy.benesse.co.jp/development/system/webpack.html),
[なぜ初心者は webpackが解らないのか？- Why can’t you understand the webpack? -](https://www.slideshare.net/ssuser46977e/webpack-why-cant-you-understand-the-webpack)