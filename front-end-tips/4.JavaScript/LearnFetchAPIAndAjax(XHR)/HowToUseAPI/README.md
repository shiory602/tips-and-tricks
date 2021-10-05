# Asynchronous and callback functions

```js
//Another example of asynchronous: do something after 1 second
const something = () => {
    console.log('Hello!') ;
};

setTimeout(something, 1000); // one second later something()
```

## Callback hell
Pile on the asynchronous, and it's not so clear at a glance.
```js
// Another example of async: greeting every second
const main = () => {
    console.log('Hello!') ;
    setTimeout(dog, 1000);
};
const dog = () => {
    console.log('Wan!') ;
    setTimeout(cat, 1000);
};
const cat = () => {
    console.log('Nyaa!') ;
    setTimeout(rabbit, 1000);
};
const rabbit = () => {
    console.log('Pyoo!') ;
};

main();
```

Console↓↓

Hello! 
Woof! 
Meow! 
Hello! 
Ta-da! 

### Callback Hell Part 2
If you use nested
```js
console.log('Hello!) ;
setTimeout(() => {
    console.log('Wan!') ;
    setTimeout(() => {
        console.log('Nyaa!') ;
        setTimeout(() => {
            console.log('Pyoo!') ;
        }, 1000);
    }, 1000);
}, 1000);
```

Console up↓↓

Hello! 
Woof! 
Meow! 
Whoa! 


# Promise
When `resolve()` is called, the callback function specified in `then()` will be called.
```js
const promise = new Promise(resolve => {
    // ... Promise's contents
    // pass resolve(value) as a callback function to the method or function that does something asynchronously
});

// ... Various 1

promise.then(value => {
    // ... Contents of then
});

// ... Various 2
```
### Order
1. Things in Promise
2. various1
3. then() (if resolve() has already been called, then execute the "contents of then")
4. Then() (if resolve() has already been called, then execute 'then contents')


# Functions to create Promise
For example, even if you create a Promise that waits for 1 second, once you use it, it is already `resolve()`, so even if you try to use it again, it will exit immediately and not wait for you the next time.
In other words, Promise needs to be renewed each time it is used.
When using Promise, it is common to define it as a function that does a new Promise, rather than just a new Promise.
```js
const doSomething = () => new Promise(resolve => {
    setTimeout(resolve, 1000, 'foo');
});
const promise = doSomething();

promise.then(value => {
    console.log({value});
});
```


***


# 非同期とコールバック関数

```js
//非同期の他の例: 1 秒後に何かする
const something = () => {
    console.log('こんにちは！');
};

setTimeout(something, 1000); // 1 秒後に something()
```

## コールバック地獄
非同期を重ねるとパッとみてよくわからなくなる。
```js
// 非同期の他の例: 1 秒ごとにあいさつ
const main = () => {
    console.log('こんにちは！');
    setTimeout(dog, 1000);
};
const dog = () => {
    console.log('わん！');
    setTimeout(cat, 1000);
};
const cat = () => {
    console.log('にゃあ！');
    setTimeout(rabbit, 1000);
};
const rabbit = () => {
    console.log('ぴょん！');
};

main();
```

コンソール↓↓

こんにちは！ 
わん！ 
にゃあ！ 
こんにちは！ 
ぴょん！ 
​
### コールバック地獄その２
入子にした場合
```js
console.log('こんにちは！');
setTimeout(() => {
    console.log('わん！');
    setTimeout(() => {
        console.log('にゃあ！');
        setTimeout(() => {
            console.log('ぴょん！');
        }, 1000);
    }, 1000);
}, 1000);
```

コンソール上↓↓

こんにちは！ 
わん！ 
にゃあ！ 
ぴょん！ 


# Promise
`resolve()` が呼ばれると `then()` に指定したコールバック関数が呼ばれる。
```js
const promise = new Promise(resolve => {
    // ... Promise の中身
    // 非同期に何かするメソッド・関数にコールバック関数として resolve(value) をわたす
});

// ... 色々1

promise.then(value => {
    // ... then の中身
});

// ... 色々2
```
### 順序
1. Promise の中身
2. 色々1
3. then() (既に resolve() が呼ばれていれば「then の中身」を実行)
4. 色々2 (resolve() が呼ばれたタイミングで「then の中身」を実行)


# Promise を作る関数
例えば、1 秒待つ Promise を作っても、一度使ってしまうと既に `resolve()` してしまっているため、使いまわそうとしても次回からはすぐに終了してしまい、待ってくれない。
つまり、Promise は使うたびに new する必要がある。
Promise を使う場合、単に new Promise するのではなく、new Promise する関数として定義するのが一般的。
```js
const doSomething = () => new Promise(resolve => {
    setTimeout(resolve, 1000, 'foo');
});
const promise = doSomething();

promise.then(value => {
    console.log({value});
});
```

参考： [Promise, async, await がやっていること (Promise と async は書き換え可能？)](https://qiita.com/kerupani129/items/2619316d6ba0ccd7be6a)