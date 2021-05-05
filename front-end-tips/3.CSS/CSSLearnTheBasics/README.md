# CSSのシンタックス

> CSSとは、`Cascading Style Sheets`の略。
> ブラウザーのエンジンがページの要素を、色、位置、装飾などの特定の特性をもって描けるようにする。

## CSSの宣言
> CSSはプロパティと値の組になっている。
> これを宣言といい、ブロックにグループ化されている。(宣言ブロック)
> ブロックは入れ子になることがあるため、左中括弧と右中括弧が対応していなければならない。
```CSS
{
    color: red;
    background-color: orange;
}
```
- プロパティ(color, background-color): 識別子。どのような特性か考えることのできる名前を定義
- 値(red, orange): 特性がどのようにエンジンに操作されなければならないか表す値

## CSSの規則セット
```CSS
p { color: red; background-color: orange; }
```
### p
セレクタ
### {} の中
Declaration Block（宣言ブロック）

## CSSの文
### 規則セット (または規則)
CSS の宣言の集合を、セレクターによって表現された状態に関連付けている文。
### アット規則
アットマーク`@`で始まり、識別子が後続し、ブロックの外のセミコロンまたは次のブロックの終わりに至るまで続く。
それぞれの種類のアット規則は、識別子によって定義され、独自の内部構文や意味を持つことがある。
**使用例**
- メタデータ情報 (`@charset` や `@import` など)
- 条件情報 (`@media` や `@document`)
- 記述的情報 (`@font-face` など)

## 基本的なセレクタの種類
### 要素の指定
HTMLタグを指定することで、装飾を施す範囲を指定。
```HTML
HTML
<p>pタグの内容</p>
<span>spanタグの内容</span>
```
```CSS
CSS
p {
    color: #F80206;
}
```
セレクタで指定してあるpタグにのみ装飾が適用され、spanタグには適用されない。

### *（すべての要素を指定）
「*（アスタリスク）」と記述することで、すべての要素に装飾が適用。
```HTML
HTML
<p>pタグの内容</p>
<span>spanタグの内容</span>
```
CSS
```CSS
* {
    color: #F80206;
}
```
先ほど同じHTMLの記述であっても、タグに関係なくすべての要素に装飾が適用。


### `.class`（クラス名の指定）
「.（ドット）クラス名」と記述することで、指定のクラスに装飾が適用。
```HTML
HTML
<p>pタグの内容</p>
<p class="example">クラス名exampleのpタグ内容</p>
<span>spanタグの内容</span><br>
<span class="example">クラス名exampleのspanタグ内容</span>
```
```CSS
CSS
.example {
    color: #F80206;
}
```
クラス名を指定するとそのクラス名が付加されている要素すべてに装飾が適用。

要素に続けてクラス名を指定することで、そのクラス名が付加された要素に装飾が適用。

```CSS
CSS
p.example {
    color: #F80206;
}
```
exampleクラスが付加されているpタグ要素にのみ、装飾が適用。


### `#id`（ID名の指定）
「#（シャープ）ID名」と記述することで、指定のIDに装飾が適用。
```HTML
HTML
<p>pタグの内容</p>
<p id="example">ID名exampleのpタグ内容</p>
<span>spanタグの内容</span><br>
<span id="example2">ID名exampleのspanタグ内容</span>
```
```CSS
CSS
p#example {
    color: #F80206;
}
```
クラス名の指定と同じく、要素に続けて指定することで、そのID名が付加された要素に装飾が適用。

## 結合子
### A B（子孫セレクタの指定）
セレクタの次に半角スペースを入れセレクタを指定することで、指定の親要素内のすべての子要素に装飾が適用。
```HTML
HTML
<p>pタグの内容</p>
<p><span>pタグの子要素のspanタグの内容</span></p>
<span>spanタグの内容</span>
```
```CSS
CSS
p span {
    color: #F80206;
}
```
ｐタグに囲われたspanタグにのみ、装飾が適用。
クラス名を指定することも可能。
```HTML
HTML
<p>pタグの内容</p>
<p><span>pタグの子要素のspanタグの内容</span></p>
<p><span class="example">pタグの子要素のクラス名exampleのspanタグの内容</span></p>
<span>spanタグの内容</span>
```
```CSS
CSS
p span.example {
    color: #F80206;
}
```
上記の例の場合は、pタグで囲われていて、かつexampleのクラス名が指定されているspanタグ要素に装飾が適用。
また、装飾の範囲は孫要素など、階層が深くなってもすべてに適用。
```HTML
HTML
<div>divタグの内容</div>
<div>
    <span>divタグの子要素のspanタグの内容</span>
    <div><p><span>divタグの孫要素のspanタグの内容</span></p></div>
</div>
<span>spanタグの内容</span>
```
```CSS
CSS
div span {
    color: #F80206;
}
```
divタグで囲われているすべてのspanタグに装飾が適用。

### A > B（子セレクタの指定）
セレクタの次に「>」を入れセレクタを指定することで、指定の親要素内の一階層下の子要素に装飾が適用。
```HTML
HTML
<div>divタグの内容</div>
<div>
    <span>divタグの子要素のspanタグの内容</span>
    <div><p><span>divタグの孫要素のspanタグの内容</span></p></div>
</div>
<span>spanタグの内容</span>
```
```CSS
CSS
div > span {
    color: #F80206;
}
```
先ほどと同じHTMLの記述であっても、divタグの一階層下にあるspanタグにのみ装飾が適用。

### A + B（隣接セレクタの指定）
セレクタの次に「+」を入れセレクタを指定することで、指定の要素に隣接した要素に装飾が適用。
```HTML
HTML
<p>pタグの内容</p>
<div>divタグの内容</div>
<p>divタグに隣接したpタグの内容</p>
<p>pタグに隣接したpタグの内容</p>
```
```CSS
CSS
div + p {
    color: #F80206;
}
```
divタグの直後にあるpタグに装飾が適用。

### A ~ B（要素の後ろにある同じ階層のセレクタの指定）
セレクタの次に「~」を入れセレクタを指定することで、指定の要素の後にある同じ階層の要素に装飾が適用。
```HTML
HTML
<p>divタグより前にあるpタグの内容</p>
<div>divタグの内容</div>
<p>divタグより後にあるpタグの内容</p>
<p>divタグより後にあるpタグの内容</p>
<div><p>divタグの子要素のpタグの内容</p></div>
<p>divタグより後にあるpタグの内容</p>
```
```CSS
CSS
div ~ p {
    color: #F80206;
}
```
divタグの以降にあるすべてのpタグに装飾が適用。ただし階層が違うと適用されない。

### A , B（複数のセレクタの指定）
セレクタの次に「,（カンマ）」を入れセレクタを指定することで、複数の要素に同じ装飾が適用。
```HTML
HTML
<div>divタグの内容</div>
<p>pタグの内容</p>
<span>spanタグの内容</span>
```CSS
CSS
div , span {
    color: #F80206;
}
```
divタグとspanタグに装飾が適用。



***

# 一般的なCSSのタグ

### fontタグ（文字の装飾）
- font-family: 文字の形
- font-size: 文字のサイズ
- color: 文字色


### backgroundタグ（背景の設定）
- background-color: 背景色
- background-image: 背景画像
- background-size: 背景画像のサイズ
- background-position: 背景画像の位置

### margin/paddingタグ（間隔を設定する）


### width/heigthタグ（幅や高さの設定）
- width: 幅を調整するタグ。
- heigth: 高さを調整するタグ。
画像の幅を調整したり、背景の高さを調整。

### borderタグ（枠線の設定）
borderは枠線を設定する要素となります。こちらも様々な種類が登場します。
```CSS
border : 2px solid #000;
```
border : (太さ) (線の種類) (線の色);



***

参照元: 
[【初心者向け】CSSセレクタとは？セレクタの種類や指定方法を解説！（基礎編）](https://www.asobou.co.jp/blog/web/css-selectors#CSS)