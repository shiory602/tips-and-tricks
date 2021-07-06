# 正規表現
> Regular expressions
文字列内を検索したり置換するための強力な方法
JavaScriptでは、正規表現は組み込みの RegExp クラスのオブジェクトを使用して実装され、文字列と統合されている。

## 構文
### 長い構文
```js
regexp = new RegExp("pattern", "flags");
```
### 短い構文
> `/`スラッシュを使う
```js
regexp = /pattern/; // フラグなし
regexp = /pattern/gmi; // g, m, i のフラグあり
```
スラッシュは正規表現を作成していることをJavaScriptに伝える、文字列の引用符と同じ役割を果たす。
- スラッシュを使用するパターンは**静的**であり、テンプレートリテラル`${..}`のような式が挿入できない
- `new RegExp`は動的に生成された文字列から**その場**で正規表現を作成する必要がある場合に使われる

## フラグ
正規表現には検索に影響を与えるフラグを含む場合がある

JavaScript のフラグは 6 つ:
| フラグ | 概要 |
| --- | --- |
| i | 検索で大文字小文字を区別しない: A と a に違いはなし。 |
| g | 検索ですべての一致を探す。指定がない場合は最初の1つのみを探す。 |
| m | 複数行モード |
| s | “dotall” モードを有効にする。これによりドット` . `が改行文字` \n `に一致できるようになる。 |
| u | 完全なユニコードサポートを有効にする。このフラグはサロゲートペアの正しい処理を可能にする。 |
| y | スティッキーモード: テキストの正確な位置で検索 |

### 検索：str.match
メソッド`str.match(regexp)`は文字列`str`中から`regexp`と一致する全ての文字列を探す
1. 正規表現にフラグ`g`がある場合、一致した全ての配列を返す
```js
let str = "We will, we will rock you";

alert( str.match(/we/gi) ); // We, we (マッチする２つの部分文字列の配列)
```
フラグ`i`は正規表現が大文字と小文字を区別しないようにするので`We`と`we`の両方が見つかる
2. 配列の形式で最初に一致したものだけを返す
```js
let str = "We will, we will rock you";
let result = str.match(/we/i); // g フラグ無し

alert( result[0] ); // We (最初の一致)
alert( result.length ); // 1

// 詳細：
alert( result.index ); // 0 (一致した位置)
alert( result.input ); // We will, we will rock you (元の文字列)
```
3. 一致するものがなかった場合は`null`が返却される（フラグ`g`の有無は関係ない）
```js
let matches = "JavaScript".match(/HTML/); // = null

if (!matches.length) { // Error: Cannot read property 'length' of null
    alert("Error in the line above");
}
```
結果を常に配列にしたい時
```js
let matches = "JavaScript".match(/HTML/) || [];

if (!matches.length) {
    alert("No matches"); // 問題なく動く
}
```
### 置換：str.replace
メソッド`str.replace(regexp, replacement)`は文字列`str`で`regexp`を使用して見つけた一致を`replacement`に置き換える（フラグ`g`があれば全ての一致を、そうでなければ最初の１つだけが対象になる）
例
```js
// g フラグ無し
alert( "We will, we will".replace(/we/i, "I") ); // I will, we will

// g フラグあり
alert( "We will, we will". replace(/we/ig, "I") ); // I will, I will
```
２番目の引数は`replacement`文字列で、特別な文字の組み合わせを使用して一致した内容の部分を挿入することもできる
| 記号 | 置換文字列での動作 |
| --- | --- |
| $& | 一致したもの全体を挿入 |
| $` | 一致の前の部分文字列を挿入 |
| $' | 一致した後の部分文字列を挿入 |
| $n | n が１−２桁の数値の場合、n番目の括弧の内容を挿入 |
| $<name> | 指定された name の括弧の中身を挿入 |
| $$ | 文字 $ を挿入 |

$& の例
```js
alert( "I love HTML".replace(/HTML/, "$& and JavaScript") ); // I love HTML and JavaScript
```

### テスト：regexp.test
メソッド`regexp.test(str)は、少なくとも１つの一致を検索し、見つかれば`true`を、なければ`false`を返す
```js
let str = "I love JavaScript";
let regexp = /LOVE/i;

alert( regexp.test(str) ); // true
```

## まとめ
- 正規表現はパターンとオプションのフラグで構成される: g, i, m, u, s, y.
- フラグと特殊記号がない場合、正規表現による検索は部分文字列検索と同じ。
- メソッド `str.match(regexp)` は一致を探す:g フラグがあればすべてを、なければ最初の1つだけが対象。
- メソッド `str.replace(regexp, replacement)` は regexp を使用して見つけた一致を replacement に置換する: g フラグがあればすべてを、なければ最初の1つだけが対象。
- メソッド `regexp.test(str)` が少なくとも1つ一致があれば true を、なければ false を返す。

***

[正規表現](https://ja.javascript.info/regexp-introduction)