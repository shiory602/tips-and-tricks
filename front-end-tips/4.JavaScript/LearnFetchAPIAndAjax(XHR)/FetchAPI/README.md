# then を使って fetch する
```js
fetch('https://jsonplaceholder.typicode.com/photos')
.then(response => response.json())
.then(postDate => console.log(postDate[0].id))
.catch(err => console.error(err));
```

# async/await を使って fetch する
```js
const getData = async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/photos");
    const data = await res.json();
    console.log(data[0].id);
  } catch (err) {
    console.log(err);
  }
};

getData();
```

[demo](https://codesandbox.io/s/fetch-async-await-try-catch-q0koh?file=/src/index.js:0-420)
参照：
[Fetch APIでデーターを取得しながらPromiseとasyc/awaitを学んだまとめ](https://qiita.com/Abbiscuit/items/66ee955509284e941803)