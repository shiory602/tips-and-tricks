# Notation of Statement
> Elements of programming language syntax are classified as expressions and statements.
## Difference between Expression and Statement
- Expression: A value can be generated and a variable can be assigned an evaluated value of that value.
```js
// Display the evaluated value of the expression 1
console.log(1);
// Assign the evaluated value of the expression to a variable
const total = 1 + 1;
// Assign the evaluated value of the function expression (function object) to a variable
const fn = function() {
  return 1;
};
// Display the evaluated value of the expression fn()
console.log(fn()); // 1
```
- Statement: Each step in a process (such as an if or for statement).
  - Distinguish between statements by writing `;` at the end of each statement line.
  - A statement cannot be assigned to a variable.
  - A statement enclosed in `{}` is called a block statement.
```js
// Combination of if statement and block statement
if (true) {
  console.log("hi");
}

// statement doesn't end in a block, so it needs a semicolon
if (true) console.log(true);
// statement ends in a block, so no semicolon needed
if (true) {
    console.log(true);
}
```
### function statements and function expressions
"A statement ending in a block doesn't need a;.
```js
// Function declaration statement to declare the learn function
function learn() {
}
// Assign the function expression to the read variable
const read = function() {
};
```
In the above expression, the anonymous function named function is an "expression", and the processing done here is part of the statement that declares the variable named **read**. Since the whole thing is an **expression**, it is necessary to add `;` at the end of the sentence.

[JavaScript Primer](https://jsprimer.net/basic/statement-expression/)
***

## Semicolon
> Always add a semicolon `;` at the end of a statement.
You can omit the semicolon, but it makes sentence breaks unclear, so it should be added unless there is a special reason.
```JS
window.alert("hello world!")
// Not an error, but deprecated.
```

## Comments
> Comments are memo-like information that is not related to the behavior of the script.
They help you get an overview of what the code is doing, what the purpose of the > description is, and so on.
> It is also useful for debugging.

### JavaScript comment syntax

| Notation | Description |
| --- | --- |
| `// comment` | Single comment. "It is recommended that you use `//` to the end of a line as a comment. |
| `/* comment */` | Multi-line comment. A block enclosed by "`/* ~ */`" is considered a comment (no nesting allowed). |
| `/** comment **/` | Documentation comment. A block surrounded by "`/** ~ */`" is regarded as a comment.

```js
// This is a comment.
/* This is a comment.
　　You can also use */
// window.alert("hello,world");
```

## Whitespaces and line breaks
If a sentence is long, you can add a line break or indent (tab/whitespace) in the middle of the sentence.
```js
window.
  alert
    ("hello, world");
```
Note that you can only start a new line after a meaningful word or symbol.
```js
win
dow.alert("hello,world");
// error
```
It is possible to write multiple statements in a single line, but it is not recommended.
Basic Statements are made on each line and terminated with `;`.
**The rule of thumb is to write only one statement per line.



### Variable
### Difference between var and let/const
- To be saved in window or not
```js
var test = "test";
let test2 = "test2";
const test3 = "test3";
console.log(window.test); // test
console.log(window.test2); // undefined
console.log(window.test3); // undefined
```
- You can also declare global variables when you declare them in a block {}.
```js
const func = () = > {
  var test = "test";
  let test2 = "test2";
  const test3 = "test3";
}
console.log(test) // test
console.log(test1) // undefined
console.log(test2) // undefined
```
- Call before declaration in Hoisting
```js
console.log(a, "a"); // Hoisted
console.log(b, "b"); // Temporal Dead Zone
console.log(c, "c"); // Temporal dead zone
var a = "1";
let b = "2";
const c = "3";
```


### let/const

## Var.
> A variable is like a box that stores values.
> Variables can be **var** or **let**.
> Use **const** for constants.

In order to use a variable, you need to declare it first.
> var variable name [= initial value] , ...
```js
var msg;
var x, y;
var msg = "hello, javascript";
```
What you can do
- Declare multiple items separated by commas
- Set the initial value in the declaration

If you don't set the initial value, the variable will be filled with **undefined** by default.
Since ES2015, let is used.


## let
Basically the same as `var`, but does not allow variables with the same name.
```js
let msg = "hi";
let msg = "hello";
// Identifier 'msg' has already been declared
```


## const
Cannot change the content.
> const constant name = value
If you want to know the tax-included price of an item with 8% sales tax, use
```js
const TAX = 1.08;
var price = 100;
console.log(price * TAX); // 108
```

### Naming Conventions
- Naming conventions for identifiers (the names given to the elements of a script)
  The first character must be one of the following: English letter, underscore (_), or dollar sign ($). 2.
  The second character must be either a letter or a number that can be used in the first character. 3.
  3. the age in the variable name is case-sensitive.
  4. not a reserved word that has a meaning in JavaScript (class, for, if, etc.)
- Main Notations of Identifiers

| Notation | Overview | Examples | Usage |
| --- | --- | --- | | --- |
| The first letter of the first word must be lower case, and the first letter of the following words must be upper case | lastName | variable/function name | Pascal notation |
| The first letter of the first word is lowercase, and the first letter of subsequent words is uppercase.
| underscore notation | concatenate words with "_" | last_name, LAST_NAME | constant name


# Data Types
Data types are the types of data.

## Major data types
## Primitive Data Types

| Data types are data types. |
| --- | --- |
| number | ±4.94065645841246544e-324 ~ ±1.79769313486231570e308 |
| A string is a set of zero or more characters enclosed in single or double quotation marks.
| boolean | true/false |
| symbol
| If you want to use an object that has the same name as the object, you can use the following methods.
| If you want to use an object with a special type, use the following type.

### Reference Types (Composite Data Types)

| Data Types |
| --- | --- |
| A set of data (each element can be accessed by an index number)
| The following table describes the types of data types that can be used in a database.
| A function is a sequence of operations (procedures).


## literal
A value itself that can be stored in a data type, or a way of representing a value.

## Numeric literals (number)
- Integer literals (integer): decimal numbers (decimals) are basic. There are also binary, octal, and hexadecimal numbers.
- Floating point literals: can be decimal or exponential.

### character literals (strings)
- Single-quote `'` and double-quote `"`: If a string contains either of these, enclose it in quotation marks of the one not included in the string.
- Escape sequences: Characters with special meanings are expressed in the form "\ + character". (Escaping)
```js
console.log('He\'s Hero!');
```
- Template strings: You can also embed variables by enclosing them in `(backtics)'.
```js
let name = "Suzuki";
let str = `Hello, ${name}-san.
It's another beautiful day! `;
console.log(str);

// Hello, Mr. Suzuki.
// It's another beautiful day!
```
- Array literal: a set of data (elements) with indices starting from 0. You can also have nested arrays as elements.
```js
var data = ["JavaScriipt", ["apple", "banana"], "Ajax", "css"];
console.log(data[1][0]); // apple
```
- Object literals: arrays that can be accessed by name as keys (the individual data are called **properties**). Also called a hash/associative array; properties with functions stored in them are called **methods**.
```js
var obj = { x:1, y:2, z:3 };
console.log(obj.x); // 1 dot operator
console.log(obj["x"]); // 1 bracket syntax
```
- function literal: A mechanism that, given an input value (argument), performs a predetermined operation and returns a result (return value).
- undefined: A value that indicates that the value of a variable is undefined.
```js
var x;
var obj = { a:12345 };
console.log(x); // undefined (no value is set)
console.log(obj.b); // undefined (property does not exist)
```
- null: no corresponding value was found (empty)


# Operators
Operators are symbols used to perform some predetermined operation on a given variable/literal.
A variable/literal that is processed by an operator is called an operand (operator).

### Arithmetic Operators
| Arithmetic Operators |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |
| ++ | Increment |
| -- | Decrement|

```JS
var num1 = 5;
var num2 = 6;

num1 + num2;
//returns 11

num2 % num1;
//returns 1
```

### Assignment Operators (assignment operators)

| Assignment Operators |
| --- | --- |
| = | Assignment Operators |
| -= | Assign subtraction |
| Assign the result of multiplication. |
| Assign a multiplication or division. |

```JS
var num1 = 7;
// num1 would return 7

num1 += 9;
// num1 would return 7 + 9 = 16
```


[W3schools](https://www.w3schools.com/js/js_syntax.asp)


***
***

# Statement（文）の記法
> プログラミング言語の構文の要素は、式と文に分類される
## ExpressionとStatementの違い
- Expression(式): 値を生成して、変数にその値の評価値を代入できるもの
```js
// 1という式の評価値を表示
console.log(1);
// 式の評価値を変数に代入
const total = 1 + 1;
// 関数式の評価値（関数オブジェクト）を変数に代入
const fn = function() {
  return 1;
};
// fn()という式の評価値を表示
console.log(fn()); // 1
```
- Statement(文): 処理をする１つ１つのステップ(if文やfor文など)
  - 文の行末に`;`を書くことで文と文を区別する
  - 文は変数に代入できない
  - 文を`{}`で囲ったものをブロック文という
```js
// if文とブロック文の組み合わせ
if (true) {
  console.log("hi");
}

// ブロックで終わらない文なので、セミコロンが必要
if (true) console.log(true);
// ブロックで終わる文なので、セミコロンが不要
if (true) {
    console.log(true);
}
```
### function文とfunction式
「ブロックで終わる文」には；は不要
```js
// learn関数を宣言する関数宣言文
function learn() {
}
// 関数式をread変数へ代入
const read = function() {
};
```
上記式では、functionという匿名関数は「式」であり、ここで行われている処理は**readという変数を宣言する文の一部**である。あくまで全体としては**式**なので文末には`;`をつける必要がある。

[JavaScript Primer](https://jsprimer.net/basic/statement-expression/)
***

## Semicolon
> 文の末尾には必ずセミコロン`;`をつける。
セミコロンは省略することもできるが、文の区切りが不明確になるので特別な理由がない限りつけるようにする。
```JS
window.alert("hello world!)
// エラーではないが非推奨
```

## Comments
> コメントとは、スクリプトの動作には関係しないメモ的な情報のこと。
> コードが何をしているのか、何を目的とした記述なのかなど、概要を把握しやすくする。
> また、デバックをする時にも有効。

### JavaScriptのコメント構文
| 記法 | 概要 |
| --- | --- |
| `// comment` | 単一コメント。「`//`」から行末までをコメントとみなす（推奨） |
| `/* comment */` | 複数行コメント。「`/* ~ */`」で囲まれたブロックをコメントとみなす（入れ子不可） |
| `/** comment **/` | ドキュメンテーションコメント。「`/** ~ */`」で囲まれたブロックをコメントとみなす |

```js
// これはコメントです。
/* こういう
　　使い方もできる */
// window.alert("hello,world");
```

## Whitespaces（空白）や改行
１つの文が長い場合は、文の途中で改行やインデント（タブ・空白）を加えることもできる。
```js
window.
  alert
    ("hello, world");
```
改行できるのは、意味ある単語や記号の後ろだけなので注意。
```js
win
dow.alert("hello,world");
// エラー
```
複数の文を単一行で書く事もできるがやらないほうがいい。
基本Statements（宣言）は１行ごとに行い`;`で終了する。
**「１行には１文だけを書く」が鉄則**



# Variable
### var と　let/const の違い
- windowに保存されるかされないか
```js
var test = "test";
let test2 = "test2";
const test3 = "test3";
console.log(window.test); // test
console.log(window.test2); // undefined
console.log(window.test3); // undefined
```
- ブロック{}内で宣言した時もグローバル変数
```js
const func = () = > {
  var test = "test";
  let test2 = "test2";
  const test3 = "test3";
}
console.log(test) // test
console.log(test1) // undefined
console.log(test2) // undefined
```
- Hoistingで宣言前に呼び出す
```js
console.log(a, "a"); // Hoisted
console.log(b, "b"); // Temporal Dead Zone
console.log(c, "c"); // Temporal dead Zone
var a = "1";
let b = "2";
const c = "3";
```


### let/const

## Var
> Variable（変数）は値を保存する箱のようなもの
> 変数には**var**と**let**がある
> 定数は**const**を使う

変数を利用するには、はじめに変数を宣言する必要がある。
> var 変数名 [= 初期値] , ...
```js
var msg;
var x, y;
var msg = ”hello, javascript";
```
できること
- 複数をカンマ区切りで宣言
- 宣言じに初期値を設定

初期値を設定しなかった場合、デフォルトで**未定義(undefined)**という値が変数にはいる。
ES2015以降はletが使われるようになった。


## let
基本的には`var`と同じだが、同名の変数を許可しない。
```js
let msg = "hi";
let msg = "hello";
// Identifier 'msg' has already been declared
```


## const
中身を変更できない。
> const 定数名 = 値
消費税８％の商品の税込価格を知りたいとき、
```js
const TAX = 1.08;
var price = 100;
console.log(price * TAX); // 108
```

### 命名規則
- 識別子（スクリプトを構成する要素につけられる名前）の命名規則
  1. １文字目は英字・アンダースコア(_)・ドル記号($)のいずれかであること
  2. ２文字目は、１文字目で使える文字、もしくは数字のいずれかであること
  3. 変数名に含まれるエイジの大文字・小文字は区別される
  4. JavaScriptで意味を持つ予約語でないこと（class,for,ifなど）
- 識別子の主な記法
| 記法 | 概要 | 例 | 使い分け |
| --- | --- | --- | --- |
| camelCase記法 | 先頭単語の頭文字は小文字、それ以降の単語の頭文字は大文字 | lastName | 変数/関数名 |
| Pascal記法 | 全ての単語の頭文字は大文字 | LastName | クラス（コンストラクター）名 |
| アンダースコア記法 | 単語同士を「_」で連結 | last_name, LAST_NAME | 定数名 |


#　Data Types
データ型とは、データの種類のこと

## 主なデータ型
### 基本型(Primitive Data Types)
| データ型 | 概要 |
| --- | --- |
| 数値型(number) | ±4.94065645841246544e-324 ~ ±1.79769313486231570e308 |
| 文字列型(string) | シングル・ダブルクオートで囲まれた０子以上の文字の集合 |
| 真偽型(boolean) | true(真)・false(偽) |
| シンボル型(symbol) | シンボルを表す |
| 特殊型(null / undefined) | 値が空、未定義であることを表す |

### 参照型(Composite Data Types)
| データ型 | 概要 |
| --- | --- |
| 配列(array) | データの集合（各要素にはインデックス番号でアクセス可能） |
| オブジェクト(object) | データの集合（各要素には名前でアクセス可能） |
| 関数(function) | 一連の処理（手続き）の集合 |


## リテラル
データ型に格納できる値そのもの、または、値の表現方法のこと。

### 数値リテラル(number)
- 整数リテラル（integer）: １０進数(decimals)が基本。他に２進数・８進数・１６進数がある。
- 浮動小数点リテラル: 小数点もしくは指数表現をとることもできる。

### 文字リテラル(string)
- シングルクオート`'`とダブルクオート`"`: 文字列の中にどちらかを含む場合は、文字列に含まれない方のクオートで囲う。
- エスケープシーケンス: 特別な意味を持つ文字は「\ + 文字」という形式で表現する。（エスケープ処理）
```js
console.log('He\'s Hero!');
```
- テンプレート文字列: `(バックティックス)で囲うと変数の埋め込みもできる。
```js
let name = "鈴木";
let str = `こんにちは、${name}さん。
今日もいい天気ですね！`;
console.log(str);

// こんにちは、鈴木さん。
// 今日もいい天気ですね！
```
- 配列リテラル: ０から始まるインデックスを持つデータ（要素）の集合。要素として配列を入れ子に持つこともできる。
```js
var data = ["JavaScriipt", ["apple", "banana"], "Ajax", "css"];
console.log(data[1][0]); // apple
```
- オブジェクトリテラル: 名前をキーにアクセスできる配列（個々のデータを**プロパティ**という）。ハッシュ・連想配列とも呼ばれ、関数が格納されたプロパティのことは、**メソッド**と呼ぶ。
```js
var obj = { x:1, y:2, z:3 };
console.log(obj.x); // 1　ドット演算子
console.log(obj["x"]); // 1　ブラケット構文
```
- 関数リテラル(function): 入力値（引数）を与えられることによって、あらかじめ決められた処理を行い、結果（戻り値）を返すしくみ
- 未定義値(undefined): 変数の値が定義されていないことを表す値。
```js
var x;
var obj = { a:12345 };
console.log(x); // undefined (値が設定されていない)
console.log(obj.b); // undefined (プロパティが存在しない)
```
- null: 該当する値がなかった（空である）


# Operators
演算子（オペレーター）とは、与えられた変数/リテラルに対して、あらかじめ決められた何らかの処理を行うための記号。
演算子によって処理される変数/リテラルのことを、オペラんと(Operand:被演算子)と呼ぶ。

### Arithmetic Operators(算術演算子)
| 演算子 | 概要 |
| --- | --- |
| + | Addition(加算) |
| - | Subtraction(減算) |
| * | Multiplication(乗算) |
| / | Division(除算) |
| % | Modulus(剰余) |
| ++ | Increment(前置加算) |
| -- | Decrement(後置減算) |

```JS
var num1 = 5;
var num2 = 6;

num1 + num2;
//returns 11

num2 % num1;
//returns 1
```

### Assignment Operators(代入演算子)
| 演算子 | 概要 |
| --- | --- |
| = | 代入 |
| += | 加算したものを代入 |
| -= | 減算したものを代入 |
| *= | 乗算したものを代入 |
| /= | 除算したものを代入 |

```JS
var num1 = 7;
// num1 would return 7

num1 += 9;
// num1 would would return 7 + 9 = 16
```


[W3schools](https://www.w3schools.com/js/js_syntax.asp)