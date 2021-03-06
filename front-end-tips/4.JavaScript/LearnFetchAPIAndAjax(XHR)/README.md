> In JavaScript, Promise is something that returns a result when an asynchronous processing operation is completed. Asynchronous processing means that you do not wait for one process to finish after it is executed, but perform another process that is coming next.(日本訳：PromiseとはJavaScriptにおいて、非同期処理の操作が完了したときに結果を返すものです。 非同期処理とは、ある処理が実行されてから終わるまで待たずに、次に控えている別の処理を行うことです。)

# Fetch API
> Features designed based on Promise (asynchronous processing) introduced in ES2015 and later.
*Asynchronous processing* here does not mean *no page transition* as in Ajax.
> Send a request to the server and load new information whenever necessary
> This is done without reloading the page.

1. execution of the API
2. set up callback functions for successful and unsuccessful communication

```js
// Execute the Fetch API
// Make a GET HTTP request with fetch -> fetch method returns a Promise instance
const userId = "any GitHub user ID";

function fetchUserInfo(userId) {
  fetch(`https://api.github.com/users/${encodeURIComponent(userId)}`)
    // When the communication is successful
    // the Promise instance is resolved in the Response object, and then the callback is invoked
    .then(response => {
        // The HTTP response status code can be obtained from the status property of the Response object
        console.log(response.status); // => 200
        // detect that an error response has been returned
        if (!response.ok) {
          console.error("Error response", response);
        } else {
          // Response object's json method also returns a Promise
          // the HTTP response body is parsed as JSON and resolved as an object
          return response.json().then(userInfo => {
              // JSON parsed*1 object is passed
              console.log(userInfo); // => {...}
          });
        }
    // When the communication fails
    // Error handling is done by the second argument of then method or the callback function of catch method
    }).catch(error => {
        console.error(error);
  });
}
```
*1: Parsing and transforming a JSON file so that it can be handled in your environment is called parse.
JSON files are just **character strings** when read as is, but we want to treat them as JavaScript objects. In other words, if you want to handle them as JSON, you can handle them as JSON by properly parsing them.

## Promise
In JavaScript, many processes are asynchronous, so callbacks are effective for letting you know when a process has finished.
However, if you use too many callbacks, you will end up with a hell of nested callbacks.
To solve this problem, **Promise** is used.

## Promise chain
In Promise, methods are called one after another with `.` Promise uses a mechanism called "method chaining", which connects methods one after another with.
In Promise, `.then(res => {...})` This is called a "Promise chain".


***

# Ajax(XHR)
"AJAX" (Asynchronous Javascript And Xml) = XMLHttpRequest
Ajax is a method of using JavaScript to communicate with the server side in an **asynchronous** manner, and dynamically rewriting parts of the page depending on the result of the communication**.
In addition to JavaScript, it can be achieved by combining existing functions** such as XML, XMLHttpRequest, and DOM.

### XMLHttpRequest
> An API that provides client-side functions for transmitting data between client and server.
> It provides an easy way to load data from a URL without reloading the entire page.
> This API allows you to update a portion of a web page without interrupting the user's work.
> (From MDN)

### JavaScript
XMLHttpRequest is a javascript built-in object and is pre-defined.
This means that asynchronous communication can only be implemented using javascript.

### DOM.
> The Document Object Model (DOM) is an API for HTML and XML documents. It provides a structural representation of a document, allowing changes to its content and display format. In short, it is a mechanism that connects web pages to scripts and programming languages.
> (from MDN)
When using Ajax to create a dynamic web page, it specifies which elements on the HTML/XML are to be changed. Therefore, DOM expands HTML and XML as a "tree structure" and conveys the information of the text to the application side, making it easier to process and change.

### XML
XML stands for Extensible Markup Language.
One of the markup languages for describing the meaning and structure of documents and data (similar to HTML)


***


The following actions can be performed without screen transitions!
1. communication with the server side: send a request to the server without reloading the page and perform another process while waiting for the response from the server
2. data exchange: request and receive "missing parts = some information required for update" from the server, and rewrite and display the part of the information
3. page update

An example is Google Maps.

## Difference between synchronous communication and asynchronous communication
In synchronous communication videos, when you search for a place you want to find, the entire page goes blank for a moment, and then it is displayed.
On the other hand, in asynchronous video, when you move the cursor to the place you want to find, the map of the destination will be displayed without reloading the page.

### Synchronous communication
Synchronous communication is a communication method that matches the timing of transmission and reception.
1. the page is reloaded
2. the next request cannot be sent until the round trip from request to response is completed, so no other operations can be performed until one process is completed.
Because the entire page is created and displayed from scratch, the client waits from the time the request is made until the response is received.

### Asynchronous Communication
Asynchronous communication is a communication method that shifts the timing of transmission and reception. 1.
(1) There is no reloading of the page, and other operations can be performed while waiting for the response.
2. even if the round trip from request to response is not completed, the next request can be sent, so it is possible to perform other operations without waiting for one process to be completed.




***See also
See also
[JavaScript Basics] Fetch API Basics](https://kde.hateblo.jp/entry/2018/10/22/010811),
[Ajax explained from a beginner's perspective](https://qiita.com/hisamura333/items/e3ea6ae549eb09b7efb9),
[JAVASCRIPT.INFO](https://ja.javascript.info/network) Translated with www.DeepL.com/Translator (free version)

***
***


# Fetch API
> ES2015以降に導入されたPromise（非同期処理）をベースに設計された機能
ここでの「非同期処理」はAjaxのような「ページを遷移しない」という意味ではない。
> 必要に応じていつでもサーバへリクエストを送信し新しい情報を読み込む
> ページをリロードすることなく行う

1. APIの実行
2. 通信が成功した時と失敗した時のコールバック関数の設定
```js
// Fetch APIの実行
// fetch で GET の HTTPリクエストを行う -> fetchメソッド は Promiseインスタンス を返す
const userId = "任意のGitHubユーザーID";

function fetchUserInfo(userId) {
  fetch(`https://api.github.com/users/${encodeURIComponent(userId)}`)
    // 通信が成功したとき
    // Promiseインスタンス は Responseオブジェクト で resolve され、 thenコールバック が呼び出される
    .then(response => {
        // Responseオブジェクト の statusプロパティ からは HTTPレスポンス のステータスコードが取得できる
        console.log(response.status); // => 200
        // エラーレスポンスが返されたことを検知する
        if (!response.ok) {
          console.error("エラーレスポンス", response);
        } else {
          // Responseオブジェクト の jsonメソッドも Promise を返す
          // HTTPレスポンスボディ を JSON としてパースしたオブジェクトでresolveされる
          return response.json().then(userInfo => {
              // JSONパース*1されたオブジェクトが渡される
              console.log(userInfo); // => {...}
          });
        }
    // 通信が失敗したとき
    // エラーハンドリングを thenメソッド の第二引数か catchメソッド のコールバック関数 で行う
    }).catch(error => {
        console.error(error);
  });
}
```
*1: 自分の環境で扱えるように解析、変換することをparseという
JSONファイルはそのまま読み込めばただの**文字列**だが、これらをJavaScriptのオブジェクトとして扱いたい。つまりJSONとして扱いたい場合、適切にパースすることによって、JSONとして扱うことができる。

## Promise
JavaScriptでは多くの処理が非同期のため、処理が終わったことを知らせるためにコールバックが有効。
しかしコールバックを使いすぎると入れ子上になってコールバック地獄になってしまう。
これを解決するのに使われるのが**Promise**である。

## Promiseチェーン
Promiseではメソッドを次々に`.`で繋いで呼び出す「メソッドチェーン」と言う仕組みを利用している。
Promiseでは`.then(res => {...})`をいくつも繋いで書くことができ、これを「Promiseチェーン」と言う



***

# Ajax(XHR)
“AJAX” (Asynchronous Javascript And Xml) = XMLHttpRequest
Ajaxとは、JavaScriptでサーバー側との通信を**非同期**で行い、通信結果によって**動的にページの一部だけ書き換える手法**のこと。
JavaScript以外にもXMLやXMLHttpRequest、DOMなど**既存の機能**を組み合わせて実現する。

### XMLHttpRequest
> クライアントとサーバーの間でデータを伝送するための機能をクライアント側で提供する API です。
> ページ全体を再読み込みすることなく、URLからデータを読み出す簡単な方法を提供します。
> このAPIによって、ユーザの作業を中断させることなくWebページの一部を更新することができます。
> (MDNより)

### JavaScript
XMLHttpRequestはjavascriptの組み込みオブジェクトであり、あらかじめ定義されている。
つまり、非同期通信はjavascriptを使わないと実装できない。

### DOM
> Document Object Model (DOM) は、HTML および XML ドキュメントのための API です。これはドキュメントの構造的な表現を提供し、内容や表示形態の変更を可能にします。端的に言えば、Web ページをスクリプトやプログラミング言語とつなぐような機構です。
> (MDNより）
Ajaxを使って動的なWebページを作成するときに、HTML・XML上のどの要素を変更するかを指定する。そこでDOMはHTMLやXMLを「ツリー構造」として展開し、アプリケーション側に文章の情報を伝え、加工や変更をしやすくする。

### XML
Extensible Markup Languageの略。
文書やデータの意味や構造を記述するためのマークアップ言語の一つ（HTMLと似たようなもの)


***


以下の動作を画面遷移なしで行うことができる！！
1. サーバー側との通信：ページの再読み込みなしにサーバーにリクエストを送信しサーバーからのレスポンスを待つ間に別の処理を行う
2. データ交換：「足りていない部分 = 更新に必要な一部の情報」をサーバーにリクエストして受け取り、その一部の情報を書き換えて表示
3. ページの更新

例に挙げるとGoogleMapなどがある。

## 同期通信と非同期崇信の違い
同期通信の動画は、探したい場所を検索すると一瞬ページ全体が真っ白になってから表示される。
一方で非同期通信の動画は、探したい場所をカーソルで移動するとページの再読み込みすることなく移動先の地図が表示される。

### 同期通信
同期通信は、送信と受信のタイミングを合わせた通信方式のこと
1. ページが再読み込みされる
2. リクエストからレスポンスの１往復が終わらないと、次のリクエストは送信できないため、１つの処理が終わるまで他の操作できない
3. ページ全体を１から作成して表示しているため、クライアントは、リクエストしてからレスポンスが返るまで待機状態になる

### 非同期通信
非同期通真は、送信と受信のタイミングをずらした通信方式のこと
1. ページの再読み込みがなく、レスポンス待ちでも別の操作をする事が出来る
2. リクエストからレスポンスの１往復が終わらなくても、次のリクエストは送信する事ができるため、１つの処理が終わるまで待たずに他の操作をする事が出来る




***
参照：
[【JavaScript基礎】Fetch APIの基礎](https://kde.hateblo.jp/entry/2018/10/22/010811),
[初心者目線でAjaxの説明](https://qiita.com/hisamura333/items/e3ea6ae549eb09b7efb9),
[JAVASCRIPT.INFO](https://ja.javascript.info/network)