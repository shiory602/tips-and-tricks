# クロージャー
> 関数と、その関数が宣言されたレキシカル環境の組み合わせ
> クロージャは関数とその関数が作られた環境という 2 つのものが一体となった特殊なオブジェクトです。 [MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Closures)

1. JavaScriptは関数の中に関数を定義する
2. JavaScriptの関数は変数として持ち運べる
3. JavaScriptの関数は親の関数の変数を使える
4. JavaScriptの関数の親とは生みの親のことである

## JavaScriptは関数の中に関数を定義する
全てのプログラミング言語で**関数の中に関数を定義できる**わけではない
```js
function outer() {
    function inner() {
        alert('hello')
    }
    inner(); //　ここがないとouter()を呼び出しても何も起こらない
}
outer();
```
## JavaScriptの関数は変数として持ち運べる
関数でできること
- 変数として代入する
- 戻り値として関数から返却する
- 関数の引数として受け取る
```js
function parent() {
function child() {
    console.log('I am a child');
}
return child;
}

// hello関数の返り値をxに代入
const x = parent();
console.log(x);

x();
//receive関数の第一引数にxを渡す
receive(x);
```
## JavaScriptの関数は親の関数の変数を使える
関数が２つあった場合、一方の関数内から他方の関数の変数を使うことはできない
```js
function parent() {
    const parent_value = 'old';

    function child() {
        // childからparentの変数は使えない
        // スコープの中と外
        const child_value = 'young';
    }

        //親は子供の変数は使えない
        console.log(child_value);

    child();
}
```
関数同士が親子関係にある場合のみ、子供から親の変数は使うことができる
```js
function parent() {
    const parent_value = 'old';

    function child() {
        const child_value = 'young';

        //自分の変数だから使えるのは当たり前
        console.log(child_value);

        // 親（=parent）の変数も使える
        console.log(parent_value);
    }

    // childを呼び出す
    child();
}
```
親の親の親・・・の変数まで使える（スコープチェーン）
```js
function grandparent() {
    const grandparent_value = 'old';

    function parent() {
        const parent_value = 'middle';

        function child() {
            const child_value = 'young';

            // 自分の値だから使える
            console.log(child_value);

            // 親の値だから使える
            console.log(parent_value);

            // 祖先の変数も使える
            console.log(grandparent_value);
        }

        // childを呼び出す
        child();
    }
    // parentを呼び出す
    parent();
}
grandparent();
```
## JavaScriptの関数の親とは生みの親のことである
関数を定義して変数に代入して持ち運んでいる状態（卵の状態）
関数を実行する＝卵から孵って雛鳥が生まれる
### 関数の親には二種類ある
- ダイナミックスコープ：実行された時の親
- レキシカルスコープ：定義された時の親
JavaScriptはレキシカルスコープを採用する
```js
function parent() {
    const parent_value = 'old';

    function child() {
        const child_value = 'young';
        console.log(child_value);
        console.log(parent_value);
    }
    return child
}

function other(v) {
    const other_value = 'hi';
    // 引数で受け取ったvを実行する
    // ここでchildが実行された時、childの「親」はparent? other?
    v();
}

const parent_return = parent();

// otherの引数vにparentの返り値、すなわちchildを渡す
other(parent_return);
```

# クロージャーとは
> 関数と、その関数が宣言されたレキシカル環境の組み合わせ
レキシカル関数とは親の関数の変数のこと。
> 親と生みの親（と祖先全員）が持っている変数を合わせてクロージャと呼ぶ。
親のことはエンクロージャと呼ぶ

## クロージャーが使われるケース
- コールバック関数（関数を作る関数）
- グローバル変数を使わずに関数に「状態」を持たせる（疑似プライベート変数）

### 関数のシグネチャ
入力と出力の定義のこと
引数の数と型、および戻り値の型のこと
決められたシグネチャの関数をコールバック関数に登録しておくと、イベント発生時にコールバック関数を呼んでくれる。
```js
addEventListener('帰宅', function(${時間}) {
    if(${時間}が14時前だったら) {
        銀行にお金を振り込みに行くように伝える
    } else if (${時間}が18時以降なら) {
        ご飯を作ってあげる
    }
})
```
時間以外の条件で処理を分けたい場合にクロージャーを使う
```js
function createCallBackFunction(${曜日}) {
    return function(${時間}) {
        if (${曜日}が日曜日でなければ) {
            if(${時間}が14時前だったら) {
                銀行にお金を振り込みに行くように伝える
            } else if (${時間}が18時以降なら) {
                ご飯を作ってあげる
            }
        }
    }
}
addEventListener('帰宅', createCallBackFunction(今日の曜日))
```
### メリット
クロージャを引数にとったり、クロージャを戻り値にすることで、
ネストの深くなったコールバック関数のネストを浅くできる


## クロージャを理解するポイント
- **関数は定義時のコンテキストで実行される**
関数は第一級オブジェクトなので、定義時のコンテキストとは異なるコンテキスト上で実行することができる
関数は定義時のコンテキストとは異なるコンテキスト上にある変数に代入された時にクロージャになる
```js
function outer() {
    return function () {
        var x = 'hello';
        alert(x);
    };
}
var f = outer();
f(); // 'hello'と表示
```
`var x = hello`の位置を外にずらしたものがクロージャー
```js
function outer() {
    var x = 'hello'; // outerのスコープ内で変数を定義

    return function () { //この関数が「クロージャ」
        alert(x); //”関数内関数"の中でouterスコープの変数を参照
    };
}
var f = outer();
f(); // 'hello'と表示
```
### クロージャが満たす条件
- outerのスコープ内で変数を定義
- outerの中に関数（＝関数内関数）を作る
- その関数内関数から先ほどの変数を参照する

***
[JavaScript猿でもわかるクロージャ超入門　まとめ
](http://dqn.sakusakutto.jp/2009/01/javascript_5.html#:~:text=%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%B8%E3%83%A3%E3%81%A8%E3%81%AF&text=%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%B8%E3%83%A3%20(%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%B8%E3%83%A3%E3%83%BC%E3%80%81Closure)%20%E3%81%AF,%E9%96%A2%E6%95%B0%E3%81%AE%E3%81%93%E3%81%A8%E3%81%A7%E3%81%82%E3%82%8B%E3%80%82),
[クロージャとは](https://qiita.com/hennin/items/806bc2633556dea85ee2),
[Youtube:プログラミングアカデミー](https://youtu.be/OY6plmd5qPE)