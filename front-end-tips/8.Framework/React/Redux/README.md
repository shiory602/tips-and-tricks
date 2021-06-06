# Redux
> Reduxとは、React.jsで使用するstateつまりアプリケーションの状態を管理するフレームワーク
> 状態管理するためのフレームワークで、例えば
> ページングがある一覧に対して、現在のページ数を保持したり、「次へ」を押して読み込んでる最中は読み込んでいるという状態を管理する。
> チェックボタンが3つあって、3つチェックされたら送信ボタンが ON になるための状態を管理するなど。
- アプリケーションの全ての状態はストアで一元管理
- ビュー(React本体)はstateとaction creatorを受け取り、stateにしたがって描画するだけ
- 描画を変えたいときはビューがactionを発動してstateを更新する。（その結果、描画が更新される）
### ビュー
ビューにはコンテナとコンポーネントの二種類がある
コンテナがReact外部とのインターフェース
- コンテナ（器）
    - ストアからコンポーネントで利用するstateを受け取る
    - コンポーネントで使用するaction creatorのリストを受け取る
- コンポーネント（部品）
    - コンテナからstateやactionのリストを渡され描画する
    - マウスクリック等のユーザーイベントがあったら対応するactionを発動する(dispatch)

### State
状態そのもの
このStateの状態を常に監視して、View部分であるReactでレンダリングを行う
```js
{
    title : '',
    count: 0
}
```

### Store
Stateの情報を保持している場所
- アプリケーションの状態を集中管理する場所（でっかいJSONの塊）
- 規模が大きい場合はstateをカテゴリ別に分類する
Twitterの例
```js
const store = {
    // セッションに関するもの
    session: {
        loggedIn: true,
        user: {
            id: "114514",
            screenName: "@mpyw",
        },
    },

    // 表示中のタイムラインに関するもの
    timeline: {
        type: "home",
        statuses: [
            {id: 1, screenName: "@mpyw", text: "hello"},
            {id: 2, screenName: "@mpyw", text: "bye"},
        ],
    },

    // 通知に関するもの
    notification: [],
}
```

### Action / Action Creator
- Action: typeをキーとして、stateを更新するための定義を書くで、更新するときはdispatch関数を実行することで状態更新する
```js
const action = {
    type : 'ADD_COUNT'
}
```
- Action Creator: 更新したい状態（新しいstate）の定義をstateではなく上書き更新したい部分だけかく
- ユーザーが何をしたいかという情報を持つオブジェクト(イベントドリブンと同じ概念)
    1. Storeに対して何かしたいときはActionを発行する
    2. Storeの門番（Reducer）がActionの発生を検知すると、Stateが更新される
```js
{
    type: "Actionの種類を一意に識別できる文字列またはシンボル",
    payload: "Actionの実行に必要な任意のデータ",
}
```
外部ファイルから参照する必要性に備えてexportもしておく
```js
export const ADD_VALUE = '@@myapp/ADD_VALUE';
export const addValue = amount => ({type: ADD_VALUE, payload: amount});
```

### Reducer
- Actionを元にStateの状態を更新するためのメソッド
- switch文中にActionで定義したstateのtypeで分岐し、ロジックをかく
- returnするものは必ず新しいobject
```js
Object.assign({}, state, {変更したいプロパティ})
```
- 以前の状態とActionを組み合わせて、新しい状態を生み出す
    - 初期状態はReducerのデフォルト引数で定義される
    - 状態を変更する際、渡されてきたstateそのものを書き換えずに、新しいものを合成するように書く
```js
// @param state 現在のステート
// @param action 変更内容
function myReducer(state, action) {
    // actionのタイプごとに、処理を分ける
    switch (action.type) {
        // ADD_COUNTの場合はcountを１増やす
        case 'ADD_COUNT':
            state = {
                ...state,
                count: state.count + 1
            }
            return state
        default: return state
    }
}
```


## ReactとReact+Reduxの違い
React単体: Reactコンポーネント自身が個別に状態管理をする
React + Redux: 状態管理する専用の場所（store）で状態管理し、Reactコンポーネントはそれを映すだけに徹する



## Reduxのデータフロー
1. ActionCreatorsによってActionを生成する
ユーザーのインプットによってComponent上からAction作成依頼がとびActionCreatorでActionが作成される
```js
// Action Creator: Actionを作成するメソッド
function testFunctionA(testStateA) {
    //Action: type項目で他のActionと区別
    return {
            type: "UpdateStateA",
            testStateA
        };
}
```
コンポーネントでActionをimportすることで、Action作成を依頼できる
```js
import { testFunctionA } from "testActionCreator";
```

2. Actionをdispatchする
dispatchすることでActionをState情報を保存している**Store**に送る
```js
// dispatch
dispatch(testFunctionA());
```

3. ReducerによってStore内のStateを更新する
引数のstateの更新をするのではなく、新しいstateのオブジェクトを返す
Actionのtypeごとに処理内容の変更が可能
```js
// Reducer
export const testReducer = ({ testStateA = "", testStateB = "" } = {}, action) => {
    switch (action.type) {
        case "UpdateStateA":
            testStateA = action.testStateA;
            break;
        case "UpdateStateB":
            testStateB = action.testStateB;
            break;
    }
    return {
        testStateA,
        testStateB
    };
};
```

4. ReactとReduxの連携しStore内のStateをComponentで参照する
mapStateToPropsを使用するとComponentのpropsにStateの中身を詰め込むことができ、それによって、Store内にあるStateを`this.props.testStateA`として使用することができる

### 全体図
Component、ActionCreator、Reducerはそれぞれ別ファイルで作成
```js
// Component
import { testFunctionA } from "testActionCreator";

class TestComponent extends Component {
    Update() {
        // dispatch
        dispatch(testFunctionA());
    }
    render(){
        ...
    }
};

// Action Creator
function testFunctionA(testStateA) {
    //Action
    return {
            type: "UpdateStateA",
            testStateA
        };
}

// Reducer
export const testReducer = ({ testStateA = "", testStateB = "" } = {}, action) => {
    switch (action.type) {
        case "UpdateStateA":
            testStateA = action.testStateA;
            break;
        case "UpdateStateB":
            testStateB = action.testStateB;
            break;
    }
    return {
        testStateA,
        testStateB
    };
};
```



***
[Redux公式](https://redux.js.org/)
[Reduxを分かりやすく解説してみた-Future Tech Blog](https://future-architect.github.io/articles/20200429/)
[フロントエンド Reduxの考え方をシンプルに理解しよう（入門記事）](https://www.yoheim.net/blog.php?q=20191201)