# React
> UIのパーツ（構成部品）を作るためのJavaScriptのフレームワーク
> フレームワークとは、WebサイトやWebサービスなどを作るときに、よく使う機能を提供するソフトウェア
### 特徴
- HTMLタグを埋め込むことが出来る
- 仮想DOMによる高速処理で他のフレームワークより早い
- コンポーネントを定義することで簡略してHTMLの要素に様々な機能を付けることが可能になる。
webアプリケーションなどでは本来アプリの画面を更新する場合、アプリ全体を更新する必要があるが、React.jsではSPA（シングルページアプリケーション）として動かせるアプリを作ることができることによりコンテンツの一部分だけを更新することが可能。
Reactで作られたアプリには、Facebook, Instagram, Skypeなどがある。
### Web開発の最新化
- モジュール化
カプセル化(Encapsulated)することで機能をひとまとまりにする
- 宣言(state)を管理しやすい
DOMを簡単に操作できる
- 効率化(Efficient)
DOM操作はjQueryよりも効率的になる
### React vs Angular
Angular
フレームワークであり完全なソリューション
- React
ライブラリでありビューのレンダリングとビューの確認のみを処理する
他のAPIを使う必要がある
## 描画の仕方
### 画面描画
ブラウザはDOM(Document Object Model)を使ってHTMLという文書（ドキュメント）を画面に描画するが、DOMを直接変更して再描画するのは複雑な処理となる。
### 仮想DOM(Virtual DOM)
ブラウザのDOMの状態をJavaScriptのオブジェクトとして管理することでブラウザに負荷をかけずに効率の良い再描画（Rendering）をするようにする。
**Reactのコンポーネント = 「状態を持つUI」**
### 差分描画
Reactを使うことで仮想DOMで差分のみを描画する
実際のDOMには関連する箇所だけが再描画される
### Reactコンポーネントが再描画を行うタイミング
- stateが変更された時
- propsが変更された時
## stateとpropsの違い
- state: コンポーネントの内部で宣言・制御される値
- props: 引数のように親から子（コンポーネント）に渡される値
### stateを使う理由
- Reactコンポーネント内の値を書き換えたい時
コンポーネント内の要素をDOMで直接書き換えてはいけない
新しい値を使って再描画（再レンダリング）させるのが正解


## Reactの使い方
実際にReactを使うための環境構築の方法としてcreate-react-appがある。
### create-react-app
下記を順番にインストール
1. Instal Homebrew
2. Instal nodebrew
3. Instal node
4. nodeの環境パスを通す(ターミナルの再起動を忘れずに)
### 起動
1. ターミナル上でReactを使いたいファイルを開く
2. `npx create-react-app ファイル名`でエンター
3. cd ファイル名で作成したファイルに移動
4. npm start

## ファイルの種類
- src
    - 開発用のファイルが格納される
    - ReactコンポーネントのJSXファイルなどはここに置く
- public
    - 静的ファイルが格納される
    - htmlファイルや画像ファイルなど
- build
    - 本番用ファイル
    - npm run buildコマンドで生成される

### インストール後にReactを使う
- npm start
    - ローカルサーバーを起動してReactアプリを確認できる
    - ホットリロード（保存で自動更新）に対応
- npm run build
    - 本番用ファイルを生成してbuildディレクトリに出力
    - srcとpublicのファイルを１つにまとめる（バンドル）
- npm run eject: 基本使わない
    - BabelやWebpackの設定を変えたいときに使う

## Sandbox
[Sandboxで簡単にReact操作](https://codesandbox.io/)

***

# JSX
- JavaScriptの拡張言語 ≠ テンプレート言語（vue.js）
- HTMLのマークアップを記述 + JavaScriptの構文が使える
- JSXは最終的にReact要素を生成する
> 使うのにはBabelが必要

## Why to use JSX?
> ReactはReact.createElementで要素を生成するが、構文がわかりにくい。JSXをすることで勝手にコンパイルされる。
> ２つの構文は同じ結果となる

- JSXは`-`を認識しないのでキャメルケースで記述する
- `{}`内で変数を扱える（JSでいう`${}`）
- 文法エラーが起きないよう必ず閉じタグ`/>`が必要
### Without JSX
```js
React.createElement(
    'button',
    {className: 'btn-blue'},
    'Click me!'
)
```
### With JSX
```js
<button className={'btn-blue'}>
    Click me!
</button>
```

# Component
JSXを返す関数をコンポーネントと呼ぶ
　コンポーネントには**Class Component**と**Functional Component**がある
### コンポーネントは分ける
- １ファイル＝１コンポーネントにすべし
- なぜコンポーネントを分けるのか
    - 責務を明確にする（なんのためのパーツか）
    - 大規模アプリでも管理しやすくする
    - 再利用する

## class component
JavaScriptクラスで書かれたコンポーネント
```js
class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>
    }
}
```
### class componentを使う理由
（React 16.8以前の理由）
1. コンポーネントのなかでオブジェクトの宣言をしたい時
2. コンポーネントのなかでライフサイクルを使う時
3. コンポーネントの中で即座に更新したい時（ライフサイクル）
**現在はhooksがあるのでファンクションコンポーネントでもライフサイクルとstateが使える。**
```jsx
class About extends React.Component {
    // Initializing
    state = {
        name: "Alice"
    };
    // using data in UI
    render() {
        <p>Name is {this.state.name}</p>
    }
}
```
クラスコンポーネントの中で`this`を使った場合、`this`はクラスを指す。

## functional component
Layoutをするのにオススメのコンポーネント
JavaScript関数で書かれたコンポーネントでアロー関数も使える。ライフサイクルは使えない。
別名：Stateless component
```js
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>
}
```
### setState
functional componentの中では`this.state.name`のように変更はできない。
```js
updateNameStudent = () => {
    this.setState({
        name: "Dodo"
    })
}
```

# JavaScriptのモジュール機能
- プログラムをモジュールという単位に分割する
- 原則は１ファイル＝１モジュール
- 必要な時に必要なモジュールのみ読み込む

```js
import Article from "./components/Article";

function App() {
    return (
        <Article
        title={'タイトル'}
        content={'中身'}
        />
    );
}
```

## default export
名前なしエクスポート
```js
// アロー関数のdefault export
const Title = (props) => {
    return <h2>{props.title}</h2>
};
export default Title;

// 名前付き関数のdefault export
export default function Title(props) {
    return <h2>{props.title}</h2>
}
```
推奨されるexport方法
１ファイル＝１export
一度宣言したアロー関数をdefault export
名前付き関数宣言と同時にdefault export

## default import
名前なしimport
```js
// Article.jsx(export元)
const Article = (props) => {
    return (
        <div>
            <h2>{props.title}</h2>
            <p>{props.content}</p>
        </div>
    );
};
export default Article;

// App.jsx(imiport先)
import Article from "./components/Article";
function App() {
    return (
        <Article
        title={'タイトル'}
        content={'コンテント'}
        />
    )
}
```
- default exportしたモジュールをそのまま読み込む
- importモジュール名from'ファイルパス'

## 名前付きexport
```js
// helper.js 便利な関数を集めたファイル
export const addTax = (price) => {
    return Math.floor(price *1.1)
}
export const getWild = () => {
    console.log('Get wild and touch')
}

// index.js
export {default as Article} from './Aricle'
export {default as Content} from './Content'
export {default as Title} from './Title'
```
defaultという名前のモジュールをTitleという名前でexport
- １ファイルから復習モジュールをexportしたい時
- Reactではエントリポイント（各コンポーネントを読み込む場所をindex.jsにまとめる）でよく使う
- エントリポイントでは別名exportも併用する

## 名前付きimport
```js
import {Content, Title} from "./index";
const Article = (props) => {
    return (
        <Article
            title={'タイトル'}
            content={'コンテント'}
        />
    )
}
```
- １ファイルから複数モジュールを読み込む
- エントリポイントから複数コンポーネントを読み込む

## Component Hierarchy(階層構造)
1. JSXは必ず階層構造になり、最上位コンポーネントは並列にできない。`return`で返せるのは１つのコンポーネントのみ。
```js
// Error
return (
    <p>Hello World!</p>
    <p>How are you?</p>
)
```
2. JSXの特殊タグである`React.Fragment`で囲むとHTMLタグと同じように記述できる。
```js
import React, { Fragment } from "react";
// OK
return (
    <React.Fragment>
        <p>Hello World!</p>
        <p>How are you?</p>
    </React.Fragment>
)
```
3. `React.Fragment`は省略可能
```js
// OK
return (
    <>
        <p>Hello World!</p>
        <p>How are you?</p>
    </>
)
```
**最上位タグが１つだけだった場合は必要ない！**


***

# Props
It is an object with data that is passed between components
全てのデータタイプを持つ
Reactは一方通行で親から子にデータがいく
### propsの渡し方
- OKな関数の渡し方
```js
<Button isPublished={isPublished} onClick={publishArticle} /> //関数自体をpropsとして渡す
<Button isPublished={isPublished} onClick={()=> publishArticle()} /> // callback関数として関数を渡す
```
- NGな関数の渡し方(無限レンダリングが起きる)
```js
<Button isPublished={isPublished} onClick={publishArticle()} /> // 関数を渡すときに実行されてレンダリングが起きる 
```

## Props in functional component
String以外では常に`{}`が必要
```js
// child comp
const Welcome = props => {
    return (
        <div>
            Hello, {props.name}.
        </div>
    )
    name="Sara"
}
```

## binding（結ぶ・くくりつける）
bindメソッドは、定義された関数に対して、**this**を代入できるメソッドで、その名の通り関数などをbind（紐づけ）することができる。
JavaScriptでは、関数内のthisは関数自体を指し、そのthisに値を設定することで、関数のプロパティ（関数に関する情報）を設定できる。



***

# LifeCycles
Methods that exist in react to execute function at the right timing of a react component life.
なんども実行されることがあるのでそれが正常なタイミングに起きるようにする。
[ライフサイクル図](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

## componentWillMount
レンダーされる前
### componendDidMount
レンダーされた直後
### componentWillReceiveProps
componentが新しいpropsを受け取ったとき
### shouldComponentUpdate
レンダーの前、新しいpropsかstateを受け取った後
### componentWillUpdate
レンダーの前、新しいpropsかstateを受け取った後
### componentDidUpdate
componentがDOMにアップデートされた後
### componentWillUnmount
componentがDOMから消える前

***

# React Hooks
> React 16.8(2019年2月9日)に追加された
> クラスを書かずにstateや他のReactの機能を使うことができる

## Syntax
コンポーネントのトップで使うこと
- count: stateの名前
- seCount: setState()の代わり
```js
import React, { useState } from 'react';

function Example() {
    const [count, setCount] = useState(0); // 0 はデフォルトの値

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount({ count: count + 1 })}>
                Click me
            </button>
        </div>
    )
}
```

Classの時
```js
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0
        };
    }

    render() {
        return (
            <div>
                <p>You clicked {this.state.count} times</p>
                <button onClick={() => this.setState({ count: this.state.count + 1 })}>
                    Click me
                </button>
            </div>
        );
    }
}
```

## useEffect
Hooksでライフサイクルを使うときで下記のものを含む
- componentDidMount
- componentDidUpdate
- componentWillUnmount


***

## react-router
> react-routerはReactのSPAでルーティング（ページ遷移）を可能にするライブラリ
> 通常SPAは１ページ内で全て完結するが、react-routerを使うとルーティング先で全く別のコンポーネントを表示することができ、複数のページが存在するようなSPAを作れる。

### インストール
```
npm i -D react-router-dom
```
インストールした後に使いたいファイルにインポートする
```js
import { BrowserRouter, Route, Link, Switch } from 'react-router-dom';
```
### BrowserRouter
react-router関連のコンポーネントは全て`<BrowserRouter></BrowserRouter>`の中で使う。
１プロジェクトにつき１回しか使えないので注意（全て入るように上の階層で使うこと）
```js
import React, { Component } from 'react';
import { BrowserRouter, Route, Link, Switch } from 'react-router-dom';

export default class App extends Component {
  render() {
    return (
      <BrowserRouter>
        {/* ここにreact-router関連のコンポーネントを全て書く */}
      </BrowserRouter>
    );
  }
}
```
### Route
`<Route />`にはルーティング先のURLと、そのURLで表示したいコンポーネントを指定
- path: 転移先のURL
- component: 表示したいコンポーネント（インポートしておく）
```js
import React, { Component } from 'react';
import { BrowserRouter, Route, Link, Switch } from 'react-router-dom';

class Root extends Component {
  render() {
    return <h1>root</h1>;
  }
}

class Page1 extends Component {
  render() {
    return <h2>Page1</h2>;
  }
}

class Page2 extends Component {
  render() {
    return <h2>Page2</h2>;
  }
}
export default class App extends Component {
  render() {
    return (
      <BrowserRouter>
        <h1>ルーティング先を選んでください</h1>
        <Route exact path="/" component={Root} />
        <Route path="/page1" component={Page1} />
        <Route path="/page2" component={Page2} />
      </BrowserRouter>
    );
  }
}
```
### exact
> 完全一致
react-routerはURLが前方一致したコンポーネントを全て表示する
上記例で`exact`がなかった場合、`/page1`にアクセスすると`<Root>`コンポーネントと`<Page1>`コンポーネントが表示されてしまう。（`/page1`というURLに`/`も`/page1`も両方前方一致するから）
これを防ぐために`exact`を入れて完全一致にする
### Link
> HTMLの`<a>`と同じような役割
> `to`でリンク先を指定することでそこへ遷移できる
- `<Link>`の中に`<a>`は入れられない
- クラスの指定もできない→中や外に`<div>`などを入れてクラスを付与する
```js
import React, { Component } from 'react';
import { BrowserRouter, Route, Link, Switch } from 'react-router-dom';

export default class App extends Component {
  render() {
    return (
      <BrowserRouter>
        <Link to="/">rootへ</Link><br />
        <Link to="/pageA">pageAへ</Link><br />
        <Link to="/pageB">pageBへ</Link>
      </BrowserRouter>
    );
  }
}
```
### Switch
> `<Switch>`は`<Route>`全体を囲んで使う
1. URLが最初に一致したコンポーネントを１つだけ表示
react-routerはURLが前方一致したコンポーネントを全て表示してしまうのを防ぐために使う
複数のコンポーネントが一致しても全部を表示せずに最初にマッチしたコンポーネント１つだけを表示
2.  URLがどれにも一致しなかった場合に表示するコンポーネントを指定
際gの`<Route>`だけ`path`を指定しないで使うことで、URLがどの`path`にも一致しなかった場合に表示するコンポーネントを指定できる
```js
import React, { Component } from 'react';
import { BrowserRouter, Route, Link, Switch } from 'react-router-dom';

class Root extends Component {
  render() {
    return <h1>rootです</h1>;
  }
}

class PageA extends Component {
  render() {
    return <h2>PageAです</h2>;
  }
}

class PageB extends Component {
  render() {
    return <h2>PageBです</h2>;
  }
}

class NotFound extends Component {
  render() {
    return <h2>404 NOT FOUND</h2>;
  }
}

export default class App extends Component {
  render() {
    return (
      <BrowserRouter>
        <h1>ルーティング先を選んでください</h1>
        <Link to="/">rootへ</Link><br />
        <Link to="/pageA">pageAへ</Link><br />
        <Link to="/pageB">pageBへ</Link>

        <Switch>
          <Route exact path="/" component={Root} />
          <Route path="/pageA" component={PageA} />
          <Route path="/pageB" component={PageB} />
          <Route component={NotFound} />{/* ←pathを指定しない */}
        </Switch>
      </BrowserRouter>
    );
  }
}
```
[【React】react-routerの使い方を丁寧に解説](https://dezanari.com/react-react-router/)


***

参照：
[Reactチュートリアル1：犬画像ギャラリーを作ろう](https://zenn.dev/likr/articles/6be53ca64f29aa035f07)

