# 配列の分割代入

ECMAScript 2015 (ES6) でサポートされた分割代入の仕組み
配列の要素を複数の変数にまとめて代入できる。

```js
const arr = [1, 2, 3];
const [x, y, z] = arr;
```

可変長の要素をまとめて最後の変数で受け取ることができる

```js
const arr = [1, 2, 3, 4, 5];
const [x, y, ...rest] = arr;

console.log(x);     //=> 1
console.log(y);     //=> 2
console.log(rest);  //=> [3, 4, 5]
```
代入する値が足りない場合は、undefined になる。
```js
const arr = [1, 2];
const [x, y, z] = arr;

console.log(x);  //=> 1
console.log(y);  //=> 2
console.log(z);  //=> undefined
```
関数のデフォルト引数のようなことも可能。
```js
const arr = [1, 2];
const [x=0, y=0, z=0] = arr;

console.log(x);  //=> 1
console.log(y);  //=> 2
console.log(z);  //=> 0
```

## 使用例

### 関数から複数の戻り値を返す（多値関数）
下記の `divrem` 関数は、割り算の結果（商と剰余）をまとめて返す。 呼び出し側では、分割代入の仕組みを使って別々の変数に結果を格納。
```js
function divrem(a, b) {
  return [Math.floor(a / b), a % b]
}

[quotient, remainder] = divrem(10, 3);
console.log(quotient, remainder);  //=> 3, 1
```

### 値のスワップ
一時変数を使わずに 2 つの変数の値をスワップ
```js
[a, b] = [b, a];
```
n 番目のフィボナッチ数を求める関数` fibonacci `の実装例
2 つの変数 `a`、`b` の値を分割代入でスワップしながら計算
```js
function fibonacci(n) {
  let a = 1, b = 1;
  for (let i = 2; i < n; ++i) {
    [a, b] = [b, a + b]
  }
  return b;
}

console.log(fibonacci(1));  //=> 1
console.log(fibonacci(2));  //=> 1
console.log(fibonacci(3));  //=> 2
console.log(fibonacci(4));  //=> 3
console.log(fibonacci(5));  //=> 5
```

***

[配列の分割代入で複数の値を同時に代入する (Array destructuring)](https://maku77.github.io/js/array/destructuring.html)