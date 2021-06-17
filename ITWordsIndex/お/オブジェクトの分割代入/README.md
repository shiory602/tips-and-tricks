# オブジェクトの分割代入
[Object destructuring](../O/objectDestructuring)

> ECMAScript 2015 で追加された分割代入の構文。オブジェクトの特定のプロパティのみを、それぞれ単独の変数で参照することができる。

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
    };
const {a, b} = obj;

console.log(a);  //=> 1
console.log(b);  //=> 2
```

通常、変数の名前は、オブジェクトのプロパティ名に合わせておく必要があるが、次のようにすれば別名を付けることも可能。

### 別名をつける
a プロパティの値を変数 newAへ
b プロパティの値を変数 newB に代入

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
    };
const {a: newA, b: newB} = obj;
// const {a, b} = obj; と省略できる

console.log(newA);  //=> 1
console.log(newB);  //=> 2
```

### デフォルト値の指定
分割代入時にデフォルト値を指定できる。
分割しようとしているオブジェクトに、プロパティが存在しない (undefined) 場合、デフォルト値が使用される。
```js
const obj = {
    a: 1,
    b: 2,
    c: 3
    };
const {a: newA, x: newX=999} = obj;

console.log(newA);  //=> 1
console.log(newX);  //=> 999
```

## 使用例

### 定数フィールドのショートカット
あるクラスが提供しているプロパティを、クラス名のプレフィックスを省略した形で参照

Math.PI 定数（円周率）を PI という短い名前で参照できるようにする
```js
const {PI} = Math;
console.log(PI * 2);  //=> 6.283185307179586
```

### for ループでのオブジェクト分割代入
```js
const books = [
  {title: 'Title1', author: 'Author1'},
  {title: 'Title2', author: 'Author2'},
  {title: 'Title3', author: 'Author3'},
];

for (const {title, author} of books) {
  console.log(`${title}, ${author}`);
}
```

### 複雑な構造のオブジェクトからプロパティを取り出す
複雑な構造のオブジェクトから必要なプロパティだけを個別の変数に取り出す

Web API などで取得した JSON データには、必要のないデータがたくさん含まれているので、必要なプロパティだけを分割代入で取り出すと、後のコードがシンプルになる。
```js
// 複雑な構造のデータ（例えば REST API で取得したデータなど）
const user = {
  id: 1,
  userName: 'Maku',
  avatar: {
    id: 'avatar123',
    url: 'http://example.com/sample.png',
  },
};

// 必要なプロパティだけを個別の変数に取り出す
const {
  userName,
  avatar: {
    id: avatarId
  }
} = user;

console.log(`${userName}, ${avatarId}`);  //=> Maku, avatar123
```

### export されたプロパティを別々に参照


***

[分割代入によりオブジェクトの特定のプロパティだけを単独変数に取得する (Object destructuring)](https://maku77.github.io/js/syntax/object-destructuring.html)