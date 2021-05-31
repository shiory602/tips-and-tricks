# Hoisting
> JavaScriptでは、関数内で宣言されたローカル変数は、全てその関数の先頭で宣言されたものとみなされる。
変数の巻き上げと言う概念[MDN](https://developer.mozilla.org/ja/docs/Glossary/Hoisting)
## Hoistingの問題点
- コードが思った通りの動作をしなくなる原因となる
```js
var myName = 'global';

function func() {
    console.log(myName); //undefined
    var myName = 'local';
    console.log(myName); //local
}
```
上記のコードは、実際には以下のコードと同じ振る舞いとなる。
```js
var myName = 'global';

function func() {
    var myName;

    console.log(myName); //undefined
    var myName = 'local';
    console.log(myName); //local
}
```
巻き上げられるのは宣言部分のみなので`var myName = 'local';`が巻き上げられ、関数の先頭で宣言されたようになる。
`var`で定義した変数は**undefined**となるが、`let/const`で宣言するとエラーがでる。
## Hoistingの解決予防策
> 関数で使用されるローカル変数は、関数の先頭で宣言する！


[知らないと怖い「変数の巻き上げ」とは？](https://analogic.jp/hoisting/),
[JavaScriptでエラーの原因となるHoisting（巻き上げ）、その仕組みをGIFアニメで分かりやすく解説](https://coliss.com/articles/build-websites/operation/javascript/javascript-visualized-hoisting.html)


***

# Event Bubbling
> 子要素で発生したイベント（クリックイベントなど）は、親や祖先要素まで伝搬し実行される。このイベントの伝搬を**バブリング**と言う。
## イベントハンドラプロセス
1. イベントが発生した時、子要素は “ターゲット要素” `(event.target) `としてラベル付けされる。
2. イベントは `addEventListener(...., true) `で割り当てられたハンドラを呼び出しながらドキュメントルートから event.target へ下りていく。
3. イベントは` on<event> `と3つ目の引数がないもしくは false の addEventListener を使って割り当てられたハンドラを実行しながら event.target からルートまで上がっていく。
### eventオブジェクトのプロパティにアクセス
- event.target： イベントを発生させた最も深い要素。
- event.currentTarget (=this)： イベントを処理する現在の要素（ハンドラを持つ要素）
- event.eventPhase： 現在のフェーズ (キャプチャリング=1, バブリング=3).
### addEventListener()
- 第１引数 -> イベントの種類を指定
- 第２引数 -> 任意のイベントが発生した時に処理する関数を指定
- 第３引数 -> イベント伝搬の方式を「true/false」で指定(通常はfalseを指定)
```js
対象要素.addEventListener( 種類, 関数, false )
```
### イベントフェーズ
イベントが発生すると下記の流れでイベント伝搬が発生する。
1. キャプチャーフェーズ：DOMツリーを辿ってルート要素から発生要素を探しに行く
2. ターゲットフェーズ：発生要素を検出する
3. バブルフェーズ：今度はルート要素まで遡る
## バブリングを止める
> stopPropagation() 子要素のイベントを親要素へ伝搬させないようにする
バブリングイベントはターゲット要素からまっすぐ上がってくる。
通常、`<html>`まで到達し、次に documentオブジェクトに移動し、いくつかのイベントは window にも到達し、そのパス上のすべてのハンドラを呼び出す。しかし、どのハンドラもイベントが完全に処理されたと判断し、バブリングを止めることができる。

こ要素のイベント関数内で、`stopPropagation()`を実行してあげることで止めることが可能。

例えば、ここで <button> をクリックしても body.onclick は動作しません。
```js
<body onclick="alert(`the bubbling doesn't reach here`)">
  <button onclick="event.stopPropagation()">Click me</button>
</body>
```

[バブリング と キャプチャリング](https://ja.javascript.info/bubbling-and-capturing)
[バブリングによるイベントの伝播](https://www.codegrid.net/articles/addeventlistener-1/)
[DOMイベントのキャプチャ/バブリングを整理する 〜 JSおくのほそ道 017](https://qiita.com/hosomichi/items/49500fea5fdf43f59c58#%E3%82%A4%E3%83%99%E3%83%B3%E3%83%88%E3%83%95%E3%82%A7%E3%83%BC%E3%82%BA%E3%81%A8%E3%81%AF)
***

# Scope
変数はプログラムの中で参照できる範囲を持つ。これを「スコープ」と呼ぶ。
例）関数の中で定義した変数は関数の外では使えないなど
スコープが複数存在する場合、優先順位は「スコープが近い順」となる。

## スコープの役割
- 変数名の競合を避ける：関数やブロックごとにスコープを分けて作ることで同じ名前の変数も別のものとなる
- メモリの消費を避ける：スコープがなければ、すべての変数がグローバルに属しプログラムから参照され続けるのでメモリを使う。

## スコープの種類
├── グローバルスコープ：関数外（トップレベル）で宣言した変数でプログラム全体から参照できる
└── ローカルスコープ：関数内で宣言した変数（関数の仮引数）で関数の中でのみ参照できる
    ├──関数スコープ：関数ごとに作られるスコープで、関数の内側からのみ利用可能なローカルスコープ
    └──ブロックスコープ：ブロックスコープ内でletまたはconstを用いて宣言した変数はブロックの内側からのみアクセスできる


[スコープの種類とその基本](https://www.codegrid.net/articles/2017-js-scope-1/),
[JavaScript のスコープを理解する](https://qiita.com/ktr1211/items/cde37452b013a4e97a37)
***

# Prototype
> prototypeに近しい概念は「継承」
> 継承とは、あるオブジェクトが他のオブジェクトの性質（メソッドやプロパティ等）を引き継ぐ仕組み
> JavaScriptのprototypeには関数が持つ**prototype**と、オブジェクトが持つ内部プロパティ**`[[prototype]]`**がある
> JavaScriptでは、全てのオブジェクトが「プロトタイプ」をベースに作られており、「プロトタイプ」という最小のオブジェクトをコピーすることで新しいオブジェクトを作る
## prototypeの性質
- prototypeは、オブジェクトの内部プロパティのひとつ。
- 内部プロパティ`[prototype]`には、何らかのオブジェクト（またはnull）が設定される。
- 内部プロパティ`[prototype]`は、あるオブジェクトが自身で保有していないプロパティを命令されたとき、自身の代わりにそのプロパティを、内部プロパティ`[prototype]`に設定されたオブジェクトから探索しに行く参照先である。
- 命令されたプロパティを自身の代わりに内部プロパティ`[prototype]`が保有している場合、オブジェクトはそれを返却する。
### 関数が持つprototype
オブジェクトで直接参照が可能：
```js
console.log(Object.prototype);
```
### オブジェクトが持つ[[Prototype]]
インスタンスの生成時、新たに生成されたオブジェクトにはコンストラクタ関数のprototypeの参照を持った内部プロパティ`[[Prototype]]`が生成される
```js
const newObj = new Object();
// newObj.[[Prototype]] = Object.prototype;
```
この`[[prototype]]`は参照することはできないが、`Object.getPrototypeOf()`や`__proto__`プロパティ（非推奨）をしようして参照することはできる
```js
const newObj = new Object();
console.log(Object.getPrototypeOf(newObj) === Object.prototype); //true
console.log(newObj.__proto__ === Object.prototype); // true
```
## prototypeの使い方
- prototypeを使ってメソッドを追加
構文
```js
クラス名.prototype.メソッド名 = function(仮引数1, 仮引数2, ...) {
    // 処理
    return;
}
```
例
```js
var Person = function(name, age) {
    this.name = name;
    this.age = age;
};

// クラスPersonのプロパティにgreetメソッドを追加する
Person.prototype.greet = function () {
    return "I'm" + this.name + ".years old";
};

// オブジェクトに対してプロトタイプのメソッドを呼び出せる
function myFunction() {
    var person1 = new Person('Mark', 25);
    console.log(person1.greet()); // I'm Mark. I'm 25 years old.
}
```
- prototypeによる敬称
例
```js
var Person = function(name, age) {
    this.name = name;
    this.age = age;
};

Person.prototype.greet = function() {
    return "I'm" + this.name + ". I'm" + this.age + "years old.";
};

function myFunction() {
    var person1 = new Person('Mark', 25);
    var person2 = new Person('Tom', 31);

    console.log(person1.greet()); // I'm Mark. I'm 25 years old.
    console.log(person2.greet()); // I'm Tom. I'm 31 years old.
}
```
敬称してデータを節約できるこの仕組みをプロトタイプチェーンという


## プロトタイプチェーン
> オブジェクトのプロパティを参照しようとした時に、そのプロパティがなければ`オブジェクト.__proto__`にプロパティを探しに行く仕組み。
> さらに`オブジェクト.__proto__`にもプロパティがなければ`オブジェクト.__proto__.__proto__`にというように`null`になるまで探しに行く。
### プロトタイプチェーンの例
```js
const newObj = {
    name: '新しいオブジェクト'
};
console.log(newObj.toString()); // [object Object]
```
1. newObj に toString() メソッドが無いか探す。
2. 見つからなかったので newObj.__proto__ つまり Object.prototype に toString() メソッドが無いか探す。
3. 見つかった為呼び出す。(newObj.__proto__.toString())
> 結果　[object Object]

### 見つからない場合の例
```js
const newObj = {name: '新しいオブジェクト'};
console.log(newObj.toArray()); // newObj.toArrayis not a function
```
1. newObj に toArray() メソッドが無いか探す。
2. 見つからなかったので newObj.__proto__ に toArray() メソッドを探す。
3. 見つからなかったので newObj.__proto__.__proto__ に…
4. newObj.__proto__.__proto__ は null なので終了。
> 結果　newObj.toArrayis not a function

### prototypeの拡張
toArrayメソッドを用意することで以下のように実行可能
```js
Object.prototype.toArray = function() {
  return Object.values(this);
}
const newObj = {name: '新しいオブジェクト'};
console.log(newObj.toArray()); // ["新しいオブジェクト"]
```


## `__proto__`のメリット
JavaScriptはオブジェクトのインスタンスは全てコピーとなる
コンストラクタに直接メソッドを追加すると、生成したインスタンスの数だけメソッドが作成され、メモリの消費が大きくなる
プロトタイプをしようすれば、暗黙的な参照が持てるのでこの問題を解決することができる
※ES2015からはclass構文が用意されているのでprototypeを使わずに敬称が行える

[【初心者向け】JavaScript prototypeの使い方と継承](https://webukatu.com/wordpress/blog/13503/)
[JavaScriptのprototypeを理解する](https://techplay.jp/column/618),
[JavaScript「prototype」とは？](https://tatsuno-system.co.jp/2020/03/16/blog_java-script/)
***

# Shadow DOM
> Web Componentsの標準仕様の一部だが、ブラウザに以前から実装されているもので、DOMツリーをカプセル化する仕組み
> 普通のDOMのことをLight DOMという
- Light DOM から独立したDOMの木構造を作成することができる
- Light DOM の木構造に追加すると一緒にレンダーできる

## メリット
- DOMの木構造が独立する
- Shadow DOMにあるNodeには`document.querySelector()`などではアクセスできないので他のコードからの動作を阻止できる
- Shadow DOM内のCSSは全て scoped CSS になり単純化する
    - Shadow DOM内のCSSはLight DOM に影響しない
    - Light DOM 内のCSSはShadow DOMに影響しない
    - Shadow DOM内のCSSでは`button`や`#someid`のようなCSS Selectorをかけるようになる
[Web Componentsについて勉強した](https://ideacase.jp/web-components/#outline__2),
[JAVASCRIPT.INFO](https://www.codegrid.net/articles/shadow-dom-1/),
[MDN](https://developer.mozilla.org/ja/docs/Web/Web_Components/Using_shadow_DOM)
***

# Strict
strictモードとは、JavaScript上のエラーを検出し、バグの少ないコーディングを目指すには便利な機能
### 使い方
1. 全体に設定する場合は一番上にコードを一行追加
```js
"use strict";
```
2. 関数に設定する場合は、関数の先頭に追加
```js
"use strict";
function test() {
    let hoge = 0;
    console.log(hoge);
}

test();
```
## エラーが出る具体例
1. グローバル変数への値の代入
変数宣言無しの変数に値を入れた時など
```js
"use strict";
function test() {
    hoge = 0; // グローバル変数
    console.log(hoge);
}

test();
```
2. 予約語を変数名に使用した時
```js
"use strict";
var public = 10000;
function fuga() {
    console.log(public);
}

fuga();
```
## 注意点
- 全体的ようで外部スクリプトがエラーになる場合がある
- ブラウザ・バージョンによっては対応していない場合がある
[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Strict_mode)