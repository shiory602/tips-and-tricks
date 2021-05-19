# ES6(ES2015)
モジュール機能はES6からJavaScriptの標準仕様として採用された。これまでは機能を分割するという概念はなかった。
### ES6のモジュール化の強み
- コンパクトなシンタックス
- モジュールの非同期読み込み
- １ファイル１モジュール
- 強制strictモード（`'use strict';`不要）
- 循環参照
- モジュールの生きた読み取り専用
## モジュールを使うために必要なステップ
1. ドランスパイル
トランスパイラ（Babelなど）を使い、ES6で書かれたJSコードをES5ベースのCommonJSやAMDなどのフォーマットとして変換する。
2. バンドル
トランスパイラによって書き出されたコードをモジュールの依存関係をみながら１つ（または複数）のJavaScriptファイルへとつなぎ合わせる
**ブラウザからは、バンドルされたファイルを読み込む。**

## Module
機能や役割別に関連性を持たせて切り離されたひとかたまりのコード群のことを「モジュール」と言う。

メリット
- 保守性：他のコードに影響しにくいので変更や拡張がしやすくなる
- 変数名の競合を防ぐ：適切な変数名を割り当てることでどの機能がどこに書かれているのか把握しやすくなる
- 再利用性：汎用性の高いモジュールを作ることで修正も一箇所で済むようになる

# モジュールファイルの作成と読み込み
モジュールファイルは作成(export)と読み込み(import)ができる。
### export
モジュールファイル側では「export」キーワードを使って変数をモジュール外部に後悔することができる。
```js
let name = 'shiori';
let birth = 0602;
let talk = function () {
    console.log('Hello');
};
```
全ての変数を外部に公開する場合
```js
export let name = 'shiori';
export let birth = 0602;
export let talk = function () {
    console.log('Hello');
};
```
１つのexportにまとめることも可能
これを「名前付きエクスポート(Named export)」と言う。
```js
let name = 'shiori';
let birth = 0602;
let talk = function () {
    console.log('Hello');
};
export {name, birth, talk};
```
### import
モジュールを利用する側のファイルではimport文を使用する。
```js
import {name} from 'ファイル名';
console.log(name); // shiori
```
複数の変数を一括してインポートすることも可能
```js
import {name, birth, talk} from 'ファイル名';
console.log(name); // shiori
console.log(birth); // 0602
console.log(talk()); // Hello
```

## Default export
モジュールファイル１つに付き、１つだけデフォルトエクスポートを定義することができる。
- モジュールの主要なエクスポート値
- エクスポート/インポートする際に変数名を必要としない。（var, let, constなどのシンタックスも不要）
- defaultキーワードの後に数値、文字列などのリテラルや関数、クラスを使用することができる
- 名前を設定していないこともあるため、importした先で名前をつけてあげる

３つ目のエクスポートでは、モジュールファイルからtalkと言う変数を読み込もうとしているがそのような変数はないので、代わりにデフォルトエクスポートが変数talkにインポートされる。
```js
// モジュール定義ファイル
export let name = 'shiori';
export let birth = 0602;
export default function () {
    console.log('Hello');
};
// モジュールを利用するファイル
import talk from 'ファイル名';
console.log(talk()); // Hello
```
一括でインポートすることも可能
```js
import talk, {hoge, fuga} from 'ファイル名';
talk(); //Hello
console.log(hoge); //hoge
console.log(fuga); //fuga
```

参照元：
[JavaScriptにおけるモジュールとimport/exportの使い方](https://analogic.jp/module-summary/)