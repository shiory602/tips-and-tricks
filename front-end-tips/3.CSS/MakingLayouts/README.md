# CSS のプロパティ

## Floats
(要素を浮かせる)
> 要素を包含ブロックの左右どちらかの側に沿うように設置し、テキストやインライン要素がその周りを回りこめるように定義する。
> 要素はウェブページの通常のフローから外れるが、 (絶対位置指定 とは対照的に) フローの一部であり続ける。

### キーワード値
- left
ブロックの左側寄る。
- right
ブロックの右側に寄る。
- none
要素は決して浮動しない。
- inline-start
ブロックの始端側に浮動。
ltr 表記では左側、 rtl 表記では右側になる。
- inline-end
ブロックの終端側に浮動。
ltr 表記では右側、 rtl 表記では左側になる。

### グローバル値
- inherit
素のプロパティの計算値を親要素から取得。
- initial
要素にプロパティの初期値 (または既定値) を設定する。
- unset
プロパティをリセットし、親から自然に継承された場合は継承値、そうでなければ初期値を設定する。

参照：
[【初心者向け！】CSS floatプロパティを図解で分かりやすく解説！](https://www.itra.co.jp/webmedia/float-property.html)

***

## Positioning
> 文書内で要素がどのように配置されるかを設定する。
> top, right, bottom, left の各プロパティが、配置された要素の最終的な位置を決める。


### Positioningの値

1. static（デフォルト）
    - 通常の位置に配置。
    - top, right, bottom, left, z-index プロパティは適用されない。

2. relative
    - 相対配置。
    - 通常の位置（static）を基準に指定した位置に配置。
    - table-*-group, table-row, table-column, table-cell, table-caption の要素における効果は未定義。

3. absolute
    - 絶対配置。
    - static以外が設定された親要素の位置を基準に、指定した位置に配置。
    - static以外の設定がない場合はwindow全体を基準に指定した位置に配置。

4. fixed
    - 絶対配置。absoluteと同じ。
    - スクロールしても指定した位置に固定。
    - 印刷文書の場合、要素は各ページの同じ位置に配置。

5. sticky
    - 初めは相対配置。
    - 指定した位置以降はfixed（絶対配置）として振る舞う。

### 要素の重なり順序を設定

- z-index: positionプロパティでstatic以外を指定している場合に適用。


参照:
[【CSS】positionについて分かりやすく解説してみた](https://haruhiko-zht.com/css_position_study/)
***



## Display
> 要素の表示形式を変更することができるプロパティ。
> ブロック要素かインライン要素かを変更することができる。
> その子要素のために使用されるレイアウト(grid/flow)、の設定もできる。

### ブロック要素とインライン要素

- block
    - ブロック要素ボックスを生成
    - 要素の前後に改行を作る

- inline
    - 前後に改行を生成しない
    - 一つ以上のインライン要素ボックスを生成
    - 次の要素も改行されず同じ行にくる


|  | ブロック要素 | インライン要素 | インラインブロック要素 |
| --- | --- | --- | --- |
| 並び方 | 縦方向に並ぶ（前後に改行あり） | 横方向にならぶ | 横方向に並ぶ |
| width/height | あり | なし（文字の長さや大きさで決まる） | あり |
| margin/padding | あり | 左右のみあり | あり |
| text-align | なし | あり（親要素に対して指定） | あり（親要素に対して指定） |
| vertical-align | なし | あり | あり |
| 例 | `<div>` `<table>` `<h1>` など前後に改行が入る要素 | `<a>` `<span>` などブロック要素の中身になる要素 |  |

参照：
[【CSS】displayの使い方を総まとめ！inlineやblockの違いは？](https://saruwakakun.com/html-css/basic/display)


***

## Box Model
> 要素に対して作成され、パディングやマージンを含む長方形のボックス定義

### ボックス内のコンテンツを制御するプロパティ
- overflow
    | プロパティ名 | 内容 |
    | --- | --- |
    | visible | コンテンツが枠からはみ出して表示 |
    | hidden | コンテンツが枠内に制限（はみ出た部分は非表示） |
    | clip | hiddenに同じ（さらにすべてのスクロールを禁止） |
    | scroll | 枠内に制限されスクロールバーが常に表示 |
    | auto | visibleに同じ。（はみ出る場合はスクロールになる） |
- overflow-x
    overflowが左右にはみ出た場合の指定
- overflow-y
    overflowが上下にはみ出た場合の指定

### ボックスの寸法を制御するプロパティ
- height: 高さ
- width: 幅
- max-height
- max-width
- min-height
- min-width

### ボックスのマージンを制御するプロパティ
- margin: ボーダーの外側
- margin-bottom
- margin-left
- margin-right
- margin-top
- margin-trim (en-US) 

### ボックスのパディングを制御するプロパティ
- padding: ボーダーの内側
- padding-bottom
- padding-left
- padding-right
- padding-top

### その他のプロパティ
- visibility: 文書のレイアウトを変更することなく要素を表示したり非表示にしたりする
- hidden: 要素のボックスは表示されずフォーカスもされないが、レイアウトは通常通り（子孫要素は visibility か visible に設定されていれば見える）


***

## CSS Grid

> それぞれの要素を囲む**Gridコンテナ**と、グリッド内に配置される**Gridアイテム**によって構成

### 基本プロパティ
```html
<div class="container">
    <header class="header">...</header>
    <main class="main">...</main>
    <aside class="sidebar">...</aside>
    <footer class="footer">...</footer>
</div>
```
1. コンテナに`display: grid`を指定
```css
.container {
    display: grid;
}
```
2. コンテナに`grid-template-rows`（横方向）、`grid-template-columns`（縦方向）を指定してグリッドの**サイズ**を決める
```css
.container {
  display: grid;
  grid-template-rows: 80px auto 100px;
  grid-template-columns: auto 200px;
}
```
3. 各アイテムに`grid-row`（横方向）、`grid-column`（縦方向）を指定して表示する**位置**を決める
```css
.header {
  grid-row: 1 / 2;
  grid-column: 1 / 3;
}
 /* 縦方向には2番目の線から3番目の線まで、横方向には1番目の線から2番目の線までの領域に配置する */
.main {
  grid-row: 2 / 3;
  grid-column: 1 / 2;
}
 
.sidebar {
  grid-row: 2 / 3;
  grid-column: 2 / 3;
}
 
.footer {
  grid-row: 3 / 4;
  grid-column: 1 / 3;
}
```

***
### コンテナに使えるプロパティ
### 名前付きのグリッド定義 grid-template-areas

各要素のareaに名前をつけてcontainerで配置を指定する。

```css
.container {
  display: grid;
  grid-template-rows: 80px auto 100px;
  grid-template-columns: auto 200px;
  grid-template-areas:
    "box1 box1"
    "box2 box3"
    "box4 box4";
}

.header {
  grid-area: box1;
}
 
.main {
  grid-area: box2;
}
 
.sidebar {
  grid-area: box3;
}
 
.footer {
  grid-area: box4;
}
```

１つにまとめることもできる↓
```css
grid-template:
    "box1 box1" 80px
    "box2 box3" auto
    "box4 box4" 100px /
    auto 200px;
```

### グリッド間の余白 gap

- gap: 縦方向と横方向のグリッド間の余白を定義
- row-gap: 縦方向のグリッド間の余白を定義
- column-gap: 横方向のグリッド間の余白を定義
pxなど数値で定義する。

### 横方向の位置 justify-content
コンテナ内におけるグリッドの横方向（インライン軸）の位置を指定

- start:	左寄せ
- center:	中央寄せ
- end:	右寄せ
- stretch:	軸の領域いっぱいにグリッドを広げる
- space-between:	均等配置 / 左右の余白無し
- space-around:	均等配置 / 左右の余白ありはアイテム間の半分
- space-evenly:	均等配置 / 左右の余白はアイテム間と同様

### 縦方向の位置 align-content
コンテナ内におけるグリッドの縦方向（ブロック軸）の位置を指定

- start:	上寄せ
- center:	中央寄せ
- end:	下寄せ
- stretch:	軸の領域いっぱいにグリッドを広げる
- space-between:	均等配置 / 上下の余白無し
- space-around:	均等配置 / 上下の余白ありはアイテム間の半分
- space-evenly:	均等配置 / 上下の余白はアイテム間と同様

***
### アイテムに使えるプロパティ
### order
並び順を指定

### 横方向の位置 justify-self
各グリッド内の横方向の位置を指定
- start:	左寄せ
- center:	中央寄せ
- end:	右寄せ
- stretch:	軸の領域いっぱいにグリッドを広げる

### 縦方向の位置 align-self
各グリッド内の縦方向の位置を指定
- start:	上寄せ
- center:	中央寄せ
- end:	下寄せ
- stretch:	軸の領域いっぱいにグリッドを広げる

参照：
[一番分かりやすいCSS Grid Layoutの使い方ガイド](https://webdesign-trends.net/entry/11086)

***

## Flex Box
> CSS Grid Layoutや、inline-blockと比べて細かい所を自動で調整したり、簡単にレイアウトを作成することができる。
> vertical-alignは使えないので注意。

### 基本プロパティ

- コンテナ（親要素）
- アイテム（子要素）

```html
<div class="container">
	<div class="item"></div>
	<div class="item"></div>
	<div class="item"></div>
</div>
```
1. CSSファイルで親要素（コンテナ）にdisplay:flexを指定
```css
.container{
	display: flex;	
}
```

### 親コンテナに使用できるプロパティ
- flex-direction: アイテムを配置する向きを指定
    - row（デフォルト）: アイテムを水平方向に左から右へと配置
    - row-reverse: アイテムを水平方向に右から左へと配置
    - column: アイテムを垂直方向に上から下へと配置
    - column-reverse: アイテムを垂直方向に下から上へと配置

- flex-wrap: アイテムの折り返しを指定する
    - nowrap（デフォルト）: アイテムを折り返さずに一列に配置
    - wrap: 複数行のアイテムを上から下へと配置
    - wrap-reverse: 複数行のアイテムを下から上へと配置

- flex-flow: アイテムの並び順(flex-direction)と折り返し(flex-wrap)を一括で指定する
```css
.container{
	flex-flow: {flex-directionの値} {flex-wrapの値};	
}
```

- justify-content: アイテムの水平方向の位置を指定する
    - flex-start（デフォルト）: アイテムを左揃えで配置
    - flex-end: アイテムを右揃えで配置
    - center: アイテムを左右中央揃えで配置
    - space-between: 両端のアイテムを余白を空けずに配置し、他の要素は均等に間隔を空けて配置
    - space-around: 両端のアイテムも含めて、均等な間隔を空けて配置

- align-items: アイテムの垂直方向の位置を指定する
    - stretch（デフォルト）: アイテムを上下の余白を埋めるように配置
    - flex-start: アイテムを上揃えで配置
    - flex-end: アイテムを下揃えで配置
    - center: アイテムを上下中央揃えで配置
    - baseline: アイテムをベースラインに合わせて配置

- align-content: アイテムの行の垂直方向の位置を指定する
    - stretch（デフォルト）: アイテムの行を余白を埋めるように配置
    - flex-start: アイテムの行を上揃えで配置
    - flex-end: アイテムの行を下揃えで配置
    - center: アイテムの行を上下中央揃えで配置
    - space-between: 最上行と最下行のアイテムを余白を空けずに配置し、他のアイテム行は均等に間隔を空けて配置
    - space-around: 最上行と最下行のアイテムを余白を空けずに配置し、他のアイテム行は均等に間隔を空けて配置

### 子アイテムに使用できるプロパティ一覧

- order: アイテムの並び順を指定
    デフォルト値は0で、マイナスを含む数値を指定できる。
```css
.item01 {order: 3;}
.item02 {order: 1;}
.item03 {order: 4;}
.item04 {order: 2;}
```

- flex-grow: アイテムの伸び率を指定
    デフォルト値は0。数値を指定することが可能。マイナスの値は指定できない。

- flex-shrink: アイテムの縮み率を指定
    デフォルト値は0。

- flex-basis: アイテムのベースの幅を指定
    デフォルト値はauto。

- flex: アイテムの伸び率(flex-grow)、縮み率(flex-shrink)、ベースの幅(flex-basis)を一括指定
```css
.item01 {flex: 1 0 20%;}
.item02 {flex: 2 0 30%;}
.item03 {flex: 1 0 50%;}
```

- align-self: アイテムの垂直方向の位置を指定
    - auto（デフォルト）: 親要素のalign-itemsの値を使用
    - flex-start: アイテムを上揃えで配置
    - flex-end: アイテムを下揃えで配置
    - center: アイテムを中央揃えで配置
    - baseline: アイテムをベースラインに合わせて配置
    - stretch: アイテムを上下の余白を埋めるように配置
    ※親要素にも指定されていた場合、子要素優先


参照：
[もう迷わない！CSS Flexboxの使い方を徹底解説](https://webdesign-trends.net/entry/8148)
***

### GridとFlexの違い

|  | Grid Layout | Flex box |
| --- | --- | --- |
| HTML | シンプル | 入れ子構造が複雑 |
| アイテムのサイズ | コンテナで指定 | 各アイテムで指定 |
| レイアウト | 複雑なレイアウトに向いている（2次元のレイアウト） | シンプルな横並びやタイルレイアウトに向いている（1次元のレイアウト） |
| グリッド間の幅指定するプロパティ | ある | ない（marginなどで幅を作ることは可能） |