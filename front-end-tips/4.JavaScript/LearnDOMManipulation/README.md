# DOM
> DOMとは「Document Object Model」の略
> HTMLやXML文書を操作するための、プログラミングインターフェース(たくさんの機能や規則)のこと。
> JavaScriptからHTMLを**動的**に変更することが可能になる。
> HTML DOMとは、HTML要素を取得したり、変更したり、挿入したり、削除したりするための基準である。

## DOMの分類
1. Core DOM：すべてのドキュメントタイプの基本となるモデル
2. XML DOM：XMLドキュメントの基本となるモデル
3. HTML DOM：HTMLドキュメントの基本となるモデル

## HTML DOMの定義
1. HTML要素をオブジェクトとして表現する
2. 全てのHTML要素のプロパティ
3. 全てのHTML要素にアクセスしうるためのメソッド
4. 全てのHTML要素のためのイベント

## DOMツリー
DOMでは対象となる文書の各要素を抽出し、それらを階層構造として扱う。
この木構造をDOMツリーと呼ぶ。

## ノード
文書を構成する要素や属性、テキストといったオブジェクトのこと。
DOMはノードを抽出・追加・置換・削除するための汎用的な手段を提供するAPI（Application Programming Interface: 関数やオブジェクトの集合）
| ノード | 概要 |
| --- | --- |
| ルートノード | ツリーの最上位に位置するノード。最上位ノード |
| 親ノード・子ノード | 上下関係にあるノード。直接繋がっているノードで、ルートノードに近いノードを親ノード、遠いノードを子ノードと呼ぶ（上下関係にあるが、直接の親子でないものを祖先ノードと子孫ノードと呼ぶ場合もある） |
| 兄弟ノード | 同じ親ノードを持つノード同士。先に書かれているものを兄ノード、後に書かれているものを弟ノードとして区別する場合もある。 |

## HTMLドキュメントオブジェクト
対象となる要素を取り出すことで下記のような操作ができるようになる
- 要素を取得して、その値を取り出す
- 処理した結果をある要素に反映させる
- 新規に作成した要素をある要素の配下に追加する

### 要素を取得する
| メソッド | 概要 |
| --- | --- |
| `document.getElementById("#id");` | id値をキーに要素を取得する |
| `document.getElementsByTagName("div");` | タグ名をキーに要素を取得する |
| `document.getElementsByClassName(".name")` | クラス名をキーに要素を取得する |
| `document.querySelector("selector")` | セレクター（条件）と合致した要素を取得する |
| `document.querySelector("selector")` | 条件に合致した要素を全て含んだNodeListオブジェクトを返す |

### 要素を変更する
| プロパティ | 概要 |
| --- | --- |
| `element.innerHTML =  new html content` | HTML要素の中身を変更する(非推奨)*1 |
| `element.textContent = value` | HTML要素の中身を変更する（HTMLコードも全てテキストとして表示） |
| `element.attribute = new value` | HTML要素の中の属性を変更する |
| `element.style.property = new style` | HTML要素のCSSスタイルを変更する |
| メソッド | 概要 |
| --- | --- |
| element.setAttribute("attribute", value) | HTML要素の属性値を変更する |

| `element.insertAdjacentText(position, text)` | テキストを、メソッドを実行した要素に対する相対的な位置*2に挿入 |
| `insertAdjacentElement` | HTML要素(element)を、メソッドを実行した要素に対する相対的な位置*1に挿入 |
*1 `innerHTML`の使用は、[クロスサイト・スクリプティング(XSS)攻撃](https://ja.wikipedia.org/wiki/%E3%82%AF%E3%83%AD%E3%82%B9%E3%82%B5%E3%82%A4%E3%83%88%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0)を許す恐れがあるので`innerHTML`は使わずに他の方法を推奨。`document.write()`も同じ。
```js
// 脆弱な例
var div = document.getElementById( "msg" );
var url = "http://example.jp/" + some_page;   // some_page は外部からコントロール可能な文字列
div.innerHTML = '<a href="' + url + '">' + url + "</a>";

// 安全な例
var div = document.getElementById( "msg" );
var url = "http://example.jp/" + some_page;   // some_page は外部からコントロール可能な文字列
var elm = document.createElement( "a" );
elm.setAttribute( "href", url );
elm.appendChild( document.createTextNode( url ) );
div.appendChild( elm );
```
*2 相対的な位置
`beforebegin`: element 本体の前。
`afterbegin`: element のすぐ内側の、最初の子要素の前。
`beforeend`: element のすぐ内側の、最後の子要素の後。
`afterend`:element 本体の後。
### 要素を追加・削除する
| メソッド | 概要 |
| --- | --- |
| `document.createElement("element")` | HTML要素を生成する |
| `document.removeChild("element")` | HTML要素を削除する |
| `document.appendChild("element")` | HTML要素を追加する |
| `document.replaceChild("new", "old")` | HTML要素を置き換える |
| `document.write("text")` | 出力する |


## イベントハンドラー
> イベントに対応してその処理内容を定義するコードの塊（関数）
> onプロパティによるイベントハンドラの設定は、同一の要素・同一のイベントに対して、複数のイベントハンドラーを紐づけられない

```js
document.getElementById(id).onclick = function(){code}
// オンクリックイベントにイベントハンドラーを追加する
```
1. イベントハンドラーの設定
```js
<タグ名 onイベント名="JavaScriptのコード">
```
2. イベントハンドラーの登録
```js
window（要素）オブジェクト.onイベント名 = function() { イベント発生時に実行すべき処理 }
```

### 主なイベント
イベント名は全て小文字で記述

- 読み込み
| イベント名 | 発生タイミング |
| abort | 画像の読み込みを中断した時 |
| load | ページ/画像の読み恋が完了した時 |
| unload | 他のページに移動する時 |

- マウス
| イベント名 | 発生タイミング |
| click | クリック時 |
| dblclick | ダブルクリック時 |
| mousedown | マウスボタンを押した時 |
| mouseup | マウスボタンを離した時 |
| mousemove | マウスポインターが移動した時 |
| mouseover | マウスポインターが要素に乗った時 |
| mouseout | マウスポインターが要素から外れた時とマウスポインタ―が子要素へ移った時 |
| mouseenter | マウスポインターが要素に乗った時 |
| mouseleave | マウスポインターが要素から外れた時とマウスポインタ―が子要素へ移った時 |
| contextmenu | コンテキストメニューが表示される前 |

- キー
| イベント名 | 発生タイミング |
| keydown | キーを押した時 |
| keypress | キーを押している時 |
| keyup | キーを話した時 |

- フォーム
| イベント名 | 発生タイミング |
| change | 内容が変更された時 |
| reset | リセットボタンを押した時 |
| submit | サブミットボタンを押した時 |

- フォーカス
| イベント名 | 発生タイミング |
| blur | 要素からフォーカスが離れた時 |
| focus | 要素がフォーカスされた時 |

- その他
| イベント名 | 発生タイミング |
| kresize | 要素のサイズを変更した時 |
| scroll | スクロールした時 |

### addEventListenerメソッド
> イベントリスナー
> 同一の要素の同一のイベントに対しても複数紐づけられるイベントハンドラー
```js
要素オブジェクト.addEventListener(イベントの種類, イベントに応じて実行すべき処理, イベントの方向)
```

### イベントハンドラとイベントリスナーの違い
onloadイベントハンドラ -> コンテンツ本体と全ての画像がロードされたところで実行
DOMContentLoadedイベントリスナ -> コンテンツ本体がロードされたところで実行（＝画像のロードを待たない）

**ページの初期化処理は、DOMContentLoadedイベントリスナで表すのが基本**

***


参照：
[JavaScript HTML DOM](https://www.w3schools.com/js/js_htmldom.asp),
[DOMとは何か？【JavaScript初心者向けにわかりやすく説明します！】](https://watablogtravel.com/document-object-model/),
[JAVASCRIPT.INFO](https://ja.javascript.info/modifying-document)