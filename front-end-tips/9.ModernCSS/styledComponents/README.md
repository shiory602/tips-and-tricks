# Styled Components
> JSでstyleを記述する**CSS in JS**のライブラリ
> styled-componentsを使うことで、Reactの**inline styling**やsassでの**styling**から２つのことが大きく変わる
ReactではDOM要素にスタイルをあてる手法
1. クラス名にCSSをあてる　-> CSSセレクタがグローバルなので大規模なWebアプリ開発には管理が大変
2. コンポーネントないにスタイルのプロパティを持ったオブジェクトを作ってそれを要素にあてる -> オブジェクト形式での記述でわかりにくい
上記の問題がないのが**styled-components**
- セレクタのスコープが明確
- 通常のCSSと変わりなく記述できる
- 通常のCSSからの移行がしやすい
- ベンダープレフィックス(-ms-/-webkit-/-moz-などの接頭辞)が自動で付く
- ステートなどの値を用いて動的にスタイルを指定できる(interpolation記法)
使うタイミング
- 同じ要素が複数合って、全く同じではないけどほぼ似てるデザインの時など…
### styled-componentsの形式
```js
const 任意の名前 = styled.要素名`CSSの記述`;
```
### 最小の指定
```js
const Button = styled.button`
color: red;
`
// render
<Button>ボタン</Button>
```

***

# 使い方
## インストールをしたら使いたいファイルの中でimportする
1. ターミナルを開いでコマンドを入力＝インストール
```
npm install --save styled-components
```
2. 使いたいコンポーネントのファイルの中で呼び出す
```js
import styled from 'styled-components'
```
## 基本的なスタイル
ボタンを押したら数が増えるカウンターアプリの例
```js
import React from 'react';
import styled from 'styled-components';
const App = () => {
  return (
    <Title>カウントするサンプルアプリです</Title> // styled-componentsでつけるスタイルの名前
  );
};
export default App;
// 名前 = styled.要素名
const Title = styled.h1`
  color: red;
  text-decoration: underline;
`;
```
## 動的なスタイル
1. onClickでstateのcountの値を変えてCountコンポーネントに渡して表示
2. ButtonWrapper（div要素）にcountプロパティを設定し、CSS内でJSを使って条件分岐
```js
import React from 'react';
import styled from 'styled-components';
import Counter from './components/counter';
const Title = styled.h1`
  color: red;
  text-decoration: underline
`;
const ButtonWrapper = styled.div`
  padding: 10px;
  background-color: rgba(0, 255, 20, 0.7);
  .button {
    margin: 0 5px;
    background-color: ${props => props.count > 1000 ? 'red' : 'blue'} // propsを引数に値を取得
  }
`;
const App = () => {
  const [count, setCount] = React.useState(0);
  return (
    <React.Fragment>
      <Title>カウントするサンプルアプリです</Title>
      <Counter count={count} />
      <ButtonWrapper count={count}>
        <input className="button" type="button" value="+1" onClick={() => setCount(count + 1)}></input>
        <input className="button" type="button" value="multiple" onClick={() => setCount(count * 2)}></input>
        <input className="button" type="button" value="reset" onClick={() => setCount(0)}></input>
      </ButtonWrapper>
    </React.Fragment>
  );
};
export default App;
```
## スタイルの再利用
**SubTitle**で**Title**のスタイルと要素を引き継いでスタイルを追加
再利用するときの形式
```js
const 任意の名前 = styled(再利用するstyled-components)`CSSの記述`;
```
引数に再利用する対象を入れることで、その要素のスタイルと要素を引き継いで使用することができる
```js
import React from 'react';
import styled from 'styled-components';
import Counter from './components/counter';
import Paper from '@material-ui/core/Paper'; // 外部からimportしたデータ
const Title = styled.h1`
  color: red;
  text-decoration: underline;
`;
// Titleを引き継ぐ
const SubTitle = styled(Title)`
  text-shadow: 1px 1px 2px silver;
`;
// material-uiのPaperにスタイルをつける例
const StyledPaper = styled(Paper)`
  margin: 10px;
`;
const ButtonWrapper = styled.div`
  padding: 10px;
  background-color: rgba(0, 255, 20, 0.7);
  .button {
    padding: 0 5px;
    background-color: ${props => props.count > 1000 ? 'red' : 'blue'}
  }
`;
const App = () => {
  const [count, setCount] = React.useState(0);
  return (
    <React.Fragment>
      <Title>カウントするサンプルアプリです</Title>
      <SubTitle>ボタンをクリックしてください</SubTitle> // この要素はTitleの再利用
      <StyledPaper>
        <Counter count={count} />
      </StyledPaper>
      <ButtonWrapper count={count}>
        <input className="button" type="button" value="+1" onClick={() => setCount(count + 1)}></input>
        <input className="button" type="button" value="multiple" onClick={() => setCount(count * 2)}></input>
        <input className="button" type="button" value="reset" onClick={() => setCount(0)}></input>
      </ButtonWrapper>
    </React.Fragment>
  );
};
export default App;
```
### その他の記法
- 擬似要素や擬似クラスの指定
```js
const Title = styled.h1`
  &::before { something: something; }
  &:hover { something: something; }
`;
```
- メディアクエリ 
```js
const Title = styled.h1`
  @media screen and (max-width: 425px) {}
`;
```

***
[styled components](https://styled-components.com/),
[styled-componentsのベーシックな使い方](https://www.fundely.co.jp/blog/tech/2020/09/16/180026/),
[Reactでstyled-componentsを使う-使い方いろいろ-](https://qiita.com/RyoTa0222/items/b35ad1ffbde9ba99354a),
[styled-componentsを使ったCSS設計](https://qiita.com/taneba/items/4547830b461d11a69a20)