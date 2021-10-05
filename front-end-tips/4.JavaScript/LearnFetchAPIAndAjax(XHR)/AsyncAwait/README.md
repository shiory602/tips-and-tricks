> 簡単に言うと、async が Promise の代わりで、await が then の代わり

# async
### アロー関数や function に async を付けると「async 関数」を定義できる
- 関数そのものが非同期に実行される (実行開始だけして、いつ終わるかは分からない)
- Promise を返す
`value = await promise;` は `promise.then(value => {});` と同義
`return` は `resolve()` 扱い (「then の中身」の return と同じ)
例外等の `throw` は `reject()` 扱い

# await
await を Promise に付けると、Promise が `resolve()` するのを待ってその値を取得する。
(実際は then() にあたることをしている。)

async が実際にやっていることは Promise と同じなため、await (後述) が含まれない async 関数は非同期処理をしない Promise と同様に意味がないものになる。その場合は async がない普通の関数と同じ動作をする。
```js
const asyncFunction = async () => {
  const promise = new Promise(resolve => {
      setTimeout(resolve, 1000, 'foo');; // 中で resolve('foo') が呼ばれる
  });

  const value = await promise; // 1 秒待機

  console.log(value);
};

asyncFunction();
```
（ await は async 関数内でないと使えない。）
※ async 関数外で await を使いたい場合は、async 即時関数 を使う
```js
(async () => {
    // ... (await を使ったコード)
})();
```

> 「async 関数定義の中に await 、その後ろに async 関数呼び出しまたは promise」


# .then を async/await に書き換える
`.then` を使った処理
1秒後に `foo` を Promise(resolve) の結果として返す
```js
const getQuote = () => new Promise(resolve => {
  setTimeout(resolve, 1000, 'foo')
});

getQuote().then((quote) => {
  console.log(quote)
}).catch((error) => {
  console.log(error)
})
```

`async/await`に書き換え
```js
const getQuote = () => new Promise(resolve -> {
  setTimeout(resolve(quote), 1000)
})

async function mainFunction() { // プログラム全体をasync関数で包みます。
  var quote = await getQuote("foo") // thenの前の関数をawait接頭辞をつけて呼び出す。
  .catch((error) => {
    console.log(error)
  }) 
  console.log(quote)
}

mainFunction()
```

## try/catch を使った error handling
```js
const getQuote = (quote) =>
new Promise((resolve) => {
  setTimeout(resolve(quote), 1000);
});

const mainFunction = async () => {
  try {
    const quote = await getQuote('foo')
    console.log(quote)
  } catch (err) {
    console.log(err)
  }
}

mainFunction()
```


参考： [Promise, async, await がやっていること (Promise と async は書き換え可能？)](https://qiita.com/kerupani129/items/2619316d6ba0ccd7be6a)