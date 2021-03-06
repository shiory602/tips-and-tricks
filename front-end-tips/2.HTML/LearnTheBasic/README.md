# HTMLのシンタックス（構文）

> HTML文書は、**要素**によって構造化されたプレーンテキストである。
> 要素は、始まりと終わりで対応するタグで囲まれている。それぞれのタグは山括弧 `<>` で始まり、終わる。
> `<img>` のように、どのようなテキストも囲めないタグを[空要素](#%E7%A9%BA%E8%A6%81%E7%B4%A0)という。
> HTMLタグは、head要素とbody要素の２つの要素だけを持つことができ、どのようにブラウザーが要素を解釈するかに影響する追加情報を提供する属性で拡張することができる。

## HTMLの基本構文

```HTML
<p class="nice">Hello world!</p>
<!-- 
    <p>: Opening tag
    class="nice": An attribute and its value
    Hello world!: Enclosed text content
    </p>: Closing tag
-->
```
- 終了タグのスラッシュ「/」を忘れない
- タグは大文字ではなく小文字で

HTML ファイルは、通常は .htm または .html という拡張子で保存され、ウェブサーバーによって提供され、どのウェブブラウザーでも表示することができます。

## 要素の入れ子（Nested）とドキュメントツリー
```HTML
<html>
    <body>
        <h1></h1>
        <h2></h2>
        <p>
            <a>
        </p>
    </body>
</html>
```
**要素の入れ子構造**: 要素の中にさらに別の要素があり、さらにその中に別の要素が入っている状態
これは言い換えると**階層構造(ドキュメントツリー)**とも見られる。

- html要素とbody要素 -> 親子関係（html要素が親要素、body要素が子要素）
- body要素内のh1要素とh2要素 -> 兄弟関係
- p要素とa要素 -> 親子関係（p要素が親要素、a要素が子要素）


## ブロック要素とインライン要素

### ブロックレベル要素
- それより前にあるいかなるコンテンツに対しても新たな行におけるコンテンツとして表示され、そのブロックの後に来るいかなるコンテンツもまた新たな行で表示される。
- ブロックレベル要素はそのウェブページの構造、たとえば段落・リスト・ナビゲーションメニュー・フッターなどを表すことに使用される傾向がある。
- ブロックレベル要素はインライン要素の中にネストされることはできないが、他のブロックレベル要素にネストされることがある。

### インライン要素
- ブロックレベル要素の中に包含され、なおかつ、段落全体やコンテンツのグループではなく、ドキュメントの内容の小さな部分だけを囲む要素。
- インライン要素はドキュメント内に新たな行を表示させない。
- 通常、`<a> 要素` (ハイパーリンク) 又は `<em>` や `<strong>` といった強調要素のように、テキスト段落の中で表示されます。


## 空要素
いくつかの要素は 1 つのタグのみで構成され、ドキュメント内で含まれている場所に何かを挿入したり埋め込むために使用されます。


## 属性(Attribute)
属性は実際のコンテンツの中で表示させたくない「要素に関する追加情報」を保有します。
```HTML
<p class="editor-note">Hello World!</p>
<!-- class="editor-note": attribute -->
```
`class`属性は、その要素に後でスタイル情報などが適用される対象であることを示すものとして使用できるような、固有の名前を持つことを許容する。

### 属性の要件

- 属性名と要素名の間に 1 つの半角スペース (その要素内にすでに 1 つ以上の属性が設定されている場合は、併せて各属性名の間)
- 属性名とそれに続く等号 (=)
- 属性値。始端から終端までをクォーテーションマーク (引用符) で囲む
    - 属性値のクオテーションマークは省略することもできるが、**半角スペース**を入れた場合コードのエラーや予期しない動作の原因となる。
    - ダブルクォート(`"`)で囲んでもシングルクォート(`'`)で囲んでも構わないが、混合させることはできない。
    - `Isn't`などの引用符を使った文章の場合は [HTML エンティティ](https://developer.mozilla.org/ja/docs/Learn/HTML/Introduction_to_HTML/Getting_started#entity_references_including_special_characters_in_html)を使用する必要がある。


### 真偽値属性

属性値のない属性のことを「**真偽値属性**」と言う。真偽値属性は一般的に属性名と同じ属性値だけを取ることができる。

（例）
`input` 要素の `disabled` 属性
 `input` 要素が "**使用不可能に**" (disabled, グレーアウト表示) なり、データを入力することができなくなる。
```HTML
<input type="text" disabled="disabled">
```
略記法
```HTML
<input type="text" disabled>
```

### HTML内の空白

半角スペース(改行)をどれ程入力しても、HTMLパーサはそれを**１つの半角スペース**として認識する。
半角スペースを沢山入力する理由は、HTMLコードの**可読性を向上**させるため。
HTMLのコードがいいフォーマット(書式)で記述されていて、１行の中に沢山タグをゴチャゴチャに詰め込まなければ、そのコードの中がどうなっているかが分かりやすくなる。

(例)どちらも同じ
```HTML
<p>Dogs are silly.</p>

<p>Dogs        are
         silly.</p>
```




***


# 一般的なHTMLタグについて学ぶ

## DOCTYPE宣言とhtml要素
```HTML
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title> タイトル </title>
    </head>
    <body>　本文　</body>
</html>
```

- **meta要素**: データそのものではなく、データに関する情報を記述。
    - 文字セットとはコンピュータで表示するために定められた**文字集合**のこと
    - ウェブブラウザが文章を解析して表示する際に参照する決まりのようなもの
    （例:日本語で書いたのにロシア語の文字セットを使うとウェブブラウザがロシア語だと思って表示してしまうので、文字化けの原因となる。）

- **title要素**: このHTML文書のタイトルを定義することが可能。


## 基本のタグ

### `<!DOCTYPE html>`
**DOCTYPE宣言の目的**
1. この文書がHTMLであること
2. HTMLのバージョンを明記すること(HTMLのバージョンごとに、そのバージョンで使用できる要素（タグ）や属性の名前などの情報が定義されている)
3. このDTD（Document Type Definition／文章の構成要素バージョン）がなにか明記すること

### `<html></html>`: `<html>` 要素
- HTML 文書は`<html>`要素 1 つだけからなる。
- HTML文書の最上位要素でありドキュメントを構成する他のすべての要素はこのタグの中に配置する必要がある。
- ドキュメントルートを定義する要素でルート要素とも呼ばれる。


### `<head></head>`: `<head>` 要素
- タイトルなど、ドキュメントにおける設定情報（メタデータ）を内包するための要素。
- このタグの中に配置された要素は通常、ブラウザの画面には表示されない。
(例)　検索結果に出したいページのキーワードや説明や、ページのスタイルを指定するための CSS や、文字エンコーディングの定義などが含まれる。


### `<meta charset="utf-8">`
- **UTF-8** という文字コードを使用しているということをブラウザーに伝えるためのものである。
- UTF-8 は世界中の自然言語の大半をカバーしている文字コード。
- 重要なこととしてあらゆるテキストコンテンツを扱うことができる。
- 文字コードとして UTF-8 を指定しない手はなく、そうしておけば後で説明する問題を回避できる。

### `<title></title>`: `<title>` 要素
- ページのタイトルを指定するもので、ページが読み込まれたブラウザーのタブに表示される。
- ページをブラウザー上でブックマークしたりお気に入りに追加したりすると `<title>` 要素の内容がページの説明として使われる。

### `<body></body>`: `<body>` 要素
- `<body> `タグはドキュメント中に一つだけ配置できる。
- この中にユーザーがページを訪問した時に表示したいコンテンツを記述する。
(例)テキスト、画像、ビデオ、ゲーム、オーディオトラック等

### a: アンカー（Anchor）
- 指定の要素に対してリンクを定義する。

### div
- ブロック要素
- 特に意味を持たないタグ
- 囲った要素をグループ化する。
- グループ化を行うことで指定した範囲の背景や文字色の変更など、スタイル（CSS）を指定することが可能。
似た用途で`<span>`タグがある。

### span
- インライン要素
- 特に意味を持たないタグ
- 「ここからここまで」を定義

### br: ブレイク（Break）
- 改行を行うための要素。
- 終了タグを必要とせず、単独で使用。

### table
- エクセルのような表組みを意味するタグ。

### tr
- 表組みの行（横方向）を定義するためのタグ。
- 前述の`<table>`タグの中に記述。
- このタグの中には`<th>`または`<td>`を配置する必要がある。

### td
- 表組みの内容を定義するタグ。
- エクセルでいうとセルにあたる要素。
- セルの内容がデータである場合はこのタグを用いる。

### th
`<td>`タグと同じく内容を定義するセルにあたる要素。
`<td>`と異なる点は、セルの内容がデータに対する見出しである場合にこのタグを用いる。


## 文章に意味を持たせるタグ

### h1 ~ h6: ヘディング（Heading）
- ブロック要素
- 文章中の見出しを定義するタグ。
- hに続く６段階の数値が見出しの重要度を表す。
- `<h1>`が最重要の大見出しとなって数値が下がるごとに小見出しとなる。

### p: パラグラフ（Paragraph）
- ブロック要素
- 文章中の段落を定義するタグ。
- ひとかたまりの文章をこのタグで囲うことでグループ化する。
- タグの後には自動的に改行が入る。

### img: イメージ（Image）
- 文章中にイメージ画像を挿入するためのタグ。
- 画像のパスや縦横サイズの指定など、このタグには様々な属性があるので留意が必要。

### strong
- 重要なテキストであると定義して、強調するためのタグ。
- SEO（検索エンジン最適化）として、重要キーワードをこのタグで囲むことによってがページ内容を理解しやすくするといった対策も存在する。

### ul: 順不同リスト（Unordered List）
- ブロック要素
- 表示順序に意味を持たないリストを定義するためのタグ。
- タグの中にはリストの項目を定義する`<li>`を配置する必要がある。
- スタイル（CSS）の指定がない場合は通常、項目の前に黒丸や白丸などのアイコンが表示される。

### ol: 順序付きリスト（Ordered List）
- ブロック要素
- 表示順序に意味を持つリストを定義するためのタグ。
- `<ul>`タグと同じくリストの項目を定義する`<li>`を配置する必要がある。
- スタイル（CSS）の指定がない場合は通常、項目の前に算用数字などのアイコンが表示される。

### li: リストアイテム（List Item）
- ブロック要素
- 前述の`<ul>`や`<ol>`のリスト項目を定義するためのタグ。


## HTML5で追加された要素

### section
- 囲った要素が１つのセクションであることを定義する。
- セクションとは文章の１つのまとまりとみなす節目。
- 仕様上、見出しを伴う意味的なグループの単位であるため、 このタグの中には見出しタグ（ `<h1>` 〜 `<h6>` ）を含める必要がある。

### article
- 囲った要素が１つのセクションであることを定義する。
- `<section>`との用途の違いは、タグで囲われた内容が単体で完結しているかという点。
(例) ブログ記事などのように単一のテーマについて書かれていて、そのセクションを切り出しても意味が成立する内容なのであれば`<section>`ではなく`<article>`を使用。

### header
- ウェブページ全体や個別のセクションの導入部分（ヘッダー）を定義する。
- 一般的にはウェブページに対するヘッダーとして`<body>`タグの直下に設置し、サイト名やロゴ、ナビゲーションなどを設置。

### footer
- ウェブページ全体や個別のセクションのフッター部分を定義する。
- 一般的にはウェブページに対するヘッダーとして`<body>`タグの直下に設置し、著作者に関する情報や関連ドキュメントへのリンク、著作権情報などを設置。

### main
- ドキュメントの主となる内容部分を定義する。
- 主題に基づいた本文部分をこのタグで囲う。

### nav: ナビゲーション（Navigation）
- ウェブページにおいて主要なナビゲーションであることを定義するタグ。
(例) ヘッダーに設置されたサイト内リンクをまとめたメニューリストなど。

### aside
- ドキュメントの主題とは関係性が薄い内容を定義する。
- 余談や補足、サイドバーに設置する関連項目などをこのタグで囲う。

## その他の目的別タグまとめ

### コンテンツの意味
- dl: 説明リストを意味するタグで、用語とその説明の定義に用いる。このタグの中には後述の`<dt>`と`<dd>`を配置する必要がある。
- dt: 説明リストにおける用語、名前の定義に用いる。
- dd: 説明リストにおける用語の説明の定義に用いる。
- figure: 図表など本文からは独立した自己完結型のコンテンツを定義するタグです。例えば、本文から参考文献として参照されるような画像や図表がこれにあたる。
- figcaption: `<figure>`のキャンプションや説明を定義するタグ。そのため、`<figure>`タグの中に配置する必要がある。

### テキストの意味
- sub: 表記規則の理由で小文字で、またはメインのテキストより小さく表示されるべきテキストの範囲を定義。
- sup: 表記規則の理由でメインのテキストよりも高い位置に、または小さく表示されるべきテキストの範囲を定義。
- ruby: 対象の単語の読み仮名を定義するタグです。このタグの中には後述の`<rt>`で読みとなるテキストを定義する必要がある。
- rt: `<ruby>`タグで囲われた単語の読み仮名を定義するタグです。


***


# id, class, style

## style属性とは？
> HTMLには**style属性**というものがあり、HTMLのデザインや装飾をすることができる。
> HTMLはページの構造を示す文書なので、現在このstyle属性によるレイアウトや装飾は推奨されていない。
> （レイアウトや装飾はCSSで行う。）

```HTML
<p style="color:red;">CSSと同じスタイルを適用できるが、基本的には使用しない。</p>
```

## id（アイディー）属性とは？
> **identity**の略で、HTMLの要素とCSSを関連付ける為の属性。
> id属性は「固有の名前」を付ける。

### id属性の使い方
```HTML
<p id="idの名前">id属性例</p>
```
要素名の右に半角空白を入れ、「id=””」とし、「” “」の中にidの名前を入れる。
id属性を使うとその要素に固有の名前を付けることができ、その要素固有のCSSを設定をすることができる。
```CSS
#id名{
  プロパティ:値;
}
```
このとき、要素名ではなく#(シャープ)id名とする。


### その他のid属性の指定方法

どちらも同じ意味を持つCSS。
下の方は、「要素名」を先頭に指定。
```CSS
#red{
  color:red;
}
p#red{
  color:red;
}
```

### id属性を使用するときの注意点
id属性は「固有の名前」を付ける為の属性。
つまり、Webページ（同じページ）に同じid名が2つ以上存在することがあってはいけない。


## class（クラス）属性とは？

> 同じCSSを複数の要素に適用したいときは、「class属性」を使用する。
> id属性と違いclass属性は同じページに何個出てきても問題ない。

### class属性の使い方
```html
<p class="classの名前">class属性例</p>
```

id属性では#を使用したが、class属性では、「.(ピリオド)」を使用。
```CSS
p{
  color:#000;
}
.red{
  color:red;
}
.blue{
  color:blue;
}
```

### その他のclass属性の指定方法
```css
.red{
  color:red;
}
p.red{
  color:red;
}
```
id属性同様、要素名をクラス名の前に付けて指定する方法もある。
上下の書き方による違いは、上は「すべてのredクラスが付けられた要素」に適用されるのに対し、下は「p要素に付けられたredクラス」に適用される点。


## idとclassの違い

1. idは1つまで、classは複数OK
2. idがセレクタの場合classよも優先度が高く`id > class`となる
3. JavaScriptを使う時はidの方が処理が早い

***


# イベントとイベントハンドラとは

1. ユーザによるキー入力、マウスボタンのクリック、表示内容の変化、状態の変化など、さまざまな状況でイベントが発生。
2. 発生したイベントはイベントキューを経由して対応するイベントハンドラに渡される。
3. イベントハンドラでは、オブジェクトのプロパティ変更やメソッドの実行などイベントの内容に応じた挙動がユーザアプリケーションで定義できる。(関数を登録できる)

## イベント
処理をやるきっかけになる外部からの刺激のことで、ソフトウェア側に通知される出来事。
利用者による入出力装置の操作だけなく、周辺機器や装置の状態の変化、外部の他のプログラムからの通知・例外やエラーの発生などを受け取ることもできる。

## イベントハンドラ
イベントが発生したときに呼び出される処理のこと。
対象となるイベントの種類や条件と、処理内容をセットで記述する。

### イベントリスナー
「イベントハンドラ」とは特に区別されずほぼ同義とみなされることが多いが、一部の言語では**イベントに一対一に結び付けられるものを**ハンドラ、**一つのイベントに対して複数の処理を対応付けられるものを**リスナと呼ぶ場合もある。

### イベントドリブン
コンピュータプログラムの開発および実行方式の一つ
利用者や外部の別のプログラムなどが引き起こす出来事に対応する形で処理を記述あるいは実行する方式。



## イベントとイベントハンドラの一覧

- マウス

| イベント | イベントハンドラ | 発生するタイミング |
| --- | --- | --- |
| click | onclick | クリックしたとき |
| dblclick | ondblclick | ダブルクリックしたとき |
| mouseup | onmouseup | マウスボタンを離したとき |
| mousedown | onmousedown | マウスボタンを押したとき |
| mousemove | onmousemove | マウスポインタが移動したとき |
| mouseover | onmouseover | マウスポインタが重なったとき |
| mouseout | onmouseout | マウスポインタが外れたとき |
| contextmenu | oncontextmenu | コンテキストメニューが表示されるとき |


- キー

| イベント | イベントハンドラ | 発生するタイミング |
| --- | --- | --- |
| keydown | onkeydown | キーを押したとき |
| keypress | onkeypress | キーが押されているとき |
| keyup | onkeyup | キーを離したとき |


- 読み込み

| イベント | イベントハンドラ | 発生するタイミング |
| --- | --- | --- |
| load | onload | 読み込みが完了したとき |
| unload | onunload | 別のページに移動するとき |
| abort | onabort | 読み込みが中断されたとき |


- フォーム

| イベント | イベントハンドラ | 発生するタイミング |
| --- | --- | --- |
| change | onchange | 内容が変更されたとき |
| reset | onreset | リセットボタンが押されたとき |
| submit | onsubmit | 送信ボタンが押されたとき |
| select | onselect | テキストが選択されたとき |
| input | oninput | input要素の値が変化したとき |


- フォーカス

| イベント | イベントハンドラ | 発生するタイミング |
| --- | --- | --- |
| blur | onblur | フォーカスが外れたとき |
| focus | onfocus | フォーカスされたとき |


- その他

| イベント | イベントハンドラ | 発生するタイミング |
| --- | --- | --- |
| resize | onresize | サイズを変更したとき |
| scroll | onscroll | スクロールしたとき |

***


参照:
[HTML を始めよう -MDN-](https://developer.mozilla.org/ja/docs/Learn/HTML/Introduction_to_HTML/Getting_started),
[Chrono Drive HTML辞典](https://html-coding.co.jp/annex/dictionary/html/),
[HTMLのstyle属性,id属性,class属性を覚えよう](https://mdstage.com/html-css/css-beginner/id-class)