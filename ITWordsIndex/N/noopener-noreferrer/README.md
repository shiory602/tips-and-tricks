# リンクをする時にaタグの中に使う

```html
<a href="http://example.com" target="_blank" rel="noopener noreferrer">
  リンク
</a>
```

## なぜ使うのか

`target="_blank"`のaタグには脆弱性がある。

遷移先から遷移元のページを不正に操作したり、オブジェクトにアクセスしたりできてしまう。
これによって、フィッシング詐欺攻撃を行う余地を生むのを防ぐ。


## noopener のみ

> The keyword indicates that any newly created top-level browsing context which results from following the hyperlink will not be an auxiliary browsing context. E.g., its window.opener attribute will be null.
> 別タブの遷移先から、window.openerを参照できなくなる（不正操作ができなくなる）。 ただし、 noreferrer に比べてブラウザのサポートは狭い。

### セキュリティ観点
元タブと新しいタブで別スレッドになるため、新しいタブから元タブへの操作を制御する。 noopenerを付けないと、JavaScriptでwindow.openerというオブジェクトが操作できるようになり、 新しいタブで開いたページから元タブのページの操作が可能。

### パフォーマンス観点
元タブと新しいタブで別スレッドになることで、ページの処理も別々になる。 そのため、新しいタブで開いたページでとても重い処理が走ったとしても、元タブのページへの影響を抑えることができます。 逆も同様で、元タブのページで重い処理を実行していても、新しいタブのページへの影響を抑制できる。

## noreferrer のみ

> It indicates that no referrer information is to be leaked when following the link and also implies the noopener keyword behavior under the same conditions.
> 遷移先のリソースから参照を送らないようにブラウザに指示を出す（非通知電話みたいな感じ）。 noopener より広いサポート範囲を持つ。


***

参照:
[aタグのrel=”noopener noreferrer”の意味とは？SEO的にどう？](https://www.marorika.com/entry/rel-noopener-noreferrer)