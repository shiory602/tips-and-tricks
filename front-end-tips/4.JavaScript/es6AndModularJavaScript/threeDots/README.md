# 残余引数
- 引数をつなげる
```js
let arr = [1, 2, 3]
let arr2 = [4, 5, 6]

console.log([...arr, ...arr2]) // [1, 2, 3, 4, 5, 6]
console.log(...arr, ...arr2) // 1, 2, 3, 4, 5, 6
```
- 文字列を配列に変換
```js
const str = 'kitty';
const newArr = [...str]; // ['k', 'i', 't', 't', 'y'];
```
- Max または Min の値
```js
const nums = [10, 9, 6, 12];
const max = Math.max(...nums); // 12
```
- 配列のコピー
```js
const allCatNames = ['chewie', 'leia', 'yoda', 'chewie', 'luke', 'leia'];
const allCatNamesCopy = [...allCatNames];
```
- 配列から重複を除く
```js
const catNames = [...new Set(allCatNames)]; // ['chewie', 'leia', 'yoda', 'luke'];
```

# 分割代入
```js

```

参照：
[今すぐ使いたいスプレッド構文、"Three-dots" Tip 集](https://qiita.com/girlie_mac/items/600b4fbce1374ed8fbcc)
[残余引数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/rest_parameters),
[分割代入](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)