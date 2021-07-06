# CSS Framework

## CSS first

- [Bootstrap](https://getbootstrap.com/)
Bootstrap is **Front-end Framework** which developed by Twitter.
It supports Responsive Web Design.
OOCSS design method that can be used by simply appending the specified class to each HTML element.
※Internet Explorer 7 and below, Firefox 3.6 and below are not supported.
### How to use
```html
<!-- The meta tag to set to prevent compatibility display, as it may be broken depending on the version. in InternetExplorer browser -->
<meta http-equiv="X-UA-Compatible" content="IE=edge">

<!-- This is a meta tag that is required to use responsive web design. -->
<meta name="viewport" content="width=device-width, initial-scale=1">
```
The important thing is to load jQuery first, rather than Bootstrap's JavaScript.
If you don't do that, the movement that uses Bootstrap's JavaScript will not work.
```html
<!-- Loading Bootstrap CSS -->
<link href="css/bootstrap.min.css" rel="stylesheet">
<!-- Loading jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
<!-- Loading Bootstrap JS -->
<script src="js/bootstrap.min.js"></script>
```

## JS based

- [ReactBootstrap](https://react-bootstrap.github.io/getting-started/introduction)
### 特徴
Fully dependent on plain Bootstrap stylesheets
Eliminates unnecessary dependencies such as jQuery
React componentized

- [Reactstrap](https://reactstrap.github.io/)
When Reactstrap is installed, bootstrap's CSS can be handled as a component by React.

- [Material UI](https://material-ui.com/ja/)
A UI component library developed based on Google's Material design.
How to use：[React入門 ～Material UI編～](https://zenn.dev/h_yoshikawa0724/articles/2020-09-24-react-material-ui)

# 比較

[Comparing bootstrap vs. react-bootstrap vs. reactstrap](https://npmcompare.com/compare/bootstrap,react-bootstrap,reactstrap)

[react-bootstrap vs reactstrap](https://www.npmtrends.com/react-bootstrap-vs-reactstrap)

react-bootstrap is more popular than reactstrap.

***

# CSS Framework

## CSS first

- [Bootstrap](https://getbootstrap.com/)
BootstrapはTwitter社が開発したCSSの「フレームワーク」
レスポンシブWebデザインに対応している
各HTML要素に指定されたclassを追記するだけで使えるOOCSS設計手法
※Internet Explorer 7以下とFirefox 3.6以下はサポートされていない。
### 使う準備
```html
<!-- InternetExplorerのブラウザではバージョンによって崩れることがあるので、互換表示をさせないために設定するmetaタグ -->
<meta http-equiv="X-UA-Compatible" content="IE=edge">

<!-- これはレスポンシブWebデザインを使うために必要なmetaタグです。 -->
<meta name="viewport" content="width=device-width, initial-scale=1">
```

重要なのは、BootstrapのJavaScriptよりも、jQueryを先に読み込むということ。
そうしなければ、BootstrapのJavaScriptを使う動きが動作しないのでご注意。
```html
<!-- BootstrapのCSS読み込み -->
<link href="css/bootstrap.min.css" rel="stylesheet">
<!-- jQuery読み込み -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
<!-- BootstrapのJS読み込み -->
<script src="js/bootstrap.min.js"></script>
```

## JS based

- [ReactBootstrap](https://react-bootstrap.github.io/getting-started/introduction)
### 特徴
プレーンBootstrapのスタイルシートに完全依存
jQueryなど不要な依存関係を廃している
Reactコンポーネント化されている

- [Reactstrap](https://reactstrap.github.io/)
Reactstrapを導入すると、bootstrapのCSSがReactでコンポーネントとして扱えるようになる。

- [Material UI](https://material-ui.com/ja/)
GoogleのMaterialデザインをベースに開発された、UIコンポーネントライブラリ
使い方の例：[React入門 ～Material UI編～](https://zenn.dev/h_yoshikawa0724/articles/2020-09-24-react-material-ui)

# 比較

[Comparing bootstrap vs. react-bootstrap vs. reactstrap](https://npmcompare.com/compare/bootstrap,react-bootstrap,reactstrap)

[react-bootstrap vs reactstrap](https://www.npmtrends.com/react-bootstrap-vs-reactstrap)

react-bootstrapの方がreactstrapよりもインストール数は多い