# CSS Module
A tool that provides a mechanism for CSS in React.
It can tie CSS in with Class in React.
It can also handle SASS.

## Features of CSS Module
1. the order in which styles are applied depends on the order of loading from JS
In CSS, if selectors have the same level of detail, the style written last has priority.
**Remedy: Visual regression testing (snapshot testing) using Storybook is required**. 2.
2. vendor prefixes are not automatically assigned
styled-components not only limits the scope of CSS class names, but also automatically assigns vendor prefixes.
**Remedy: You need to apply it yourself or install a separate tool. **.
3. change classes according to conditions
As with normal CSS, it is necessary to change class names dynamically depending on conditions.
**Remedy: Use `classnames`**.



## How to use
First, you need to install CSS Module.
```
$ npm init -y
$ npm install --save react react-dom
$ npm install --save-dev webpack style-loader css-loader sass-loader node-sass extract-text-webpack-plugin
$ npm install --save-dev resolve-url resolve-url-loader babel-plugin-transform-decorators-legacy
```


***



# CSS Module

ReactにおけるCSSの仕組みを提供するツールです。
CSSをReactのClassと結びつけることができます。
また、SASSを扱うこともできます。

## CSS Module の特徴
1. JS からの読み込み順序によってスタイル適用順序が変わる
CSSは詳細度が同じセレクタの場合、最後に記述したスタイルが優先される仕様になっているため、このUnify時における各CSSファイルの結合順序が、生成されるCSSファイル内のスタイル順序となる。
**対処法： Storybook を用いたビジュアルリグレッションテスト（スナップショットテスト）が必須**
2. ベンダープレフィックス（接頭辞）が自動で付与されない
styled-components では CSS クラス名のスコープを限定してくれるだけでなく、ベンダープレフィックスも自動付与してくれる。
**対処法：自分で適用するか、別途ツールを導入する必要がある。**
3. 条件によってクラスを変更する
通常のCSSと同様、条件によってクラス名を動的に変更する必要がある。
**対処法： `classnames`を使う**
```js
import styles from "./styles.css";

const Component = (props) => (
  <div className={classnames(styles.header, { [styles.disabled]: props.isDisabled })} />
);
```


***

[CSS Module](https://github.com/gajus/react-css-modules),
[styled-components（CSS in JS）をやめた理由と、不完全なCSS Modulesを愛する方法](https://qiita.com/jagaapple/items/7f74fc32c69f5b731159)