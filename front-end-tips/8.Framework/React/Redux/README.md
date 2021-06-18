# Redux
> Reduxとは、React.jsで使用するstateつまりアプリケーションの状態を管理するフレームワーク

## なぜ Redux を使うのか
1. state の見通しをよくするため
2. どこからでも state を参照/変更可能にするため
3. モジュール（機能の塊）を疎結合にするため = 機能Aと機能Bが互いに影響し合わない状態にする

## Fluxフローとは
1. データフロー設計の１つ
2. データが常に一方向に流れる
3. イベントによってデータが変化（イベント駆動）
Flux思想をReactの状態管理に適用したライブラリ＝Redux

### Flux フローの流れ（例）
1. ユーザーがウェブサイトにアクセスするとURLに応じた（コンポーネントが入っている）containerが表示される
2. 購入のcomponentをクリックすることでイベントが発生する -> Action が実行される（状態の変更）
3. Action が要求を受けて Reducer に変更の内容を伝える
4. Reducer が変更の内容を受け付けて Store でどのように状態の保存を書き換えるかを伝える
5. Store の中で状態が書き換わる
6. 書き換わった Store が `mapStateToProps/mapDispatchToProps` を通して container に伝わる
7. container の中で書き換わったデータが表示される

## Actionとは
> 要求を受けて変更を依頼
### 役割
アプリからStoreへデータを送るためのpayloadを渡す役割
- payload: データの塊（この状態をこう変更してね）
Reducer（変更の管理人）にtype(どんな変更の種類)とpayload(どんなデータの種類)を返す
### 使い方
1. Action type を定義して export -> reducer で以来の種類を import
2. type と payload を記述する
3. Actions は常に**プレーン**な object を返す(処理しない)
```js
//　1.Action type を定義して export -> reducer で import
export const SIGN_IN = "SIGN_IN";

export const signInAction = (userState) => {
    // 3.プレーンな object を返す
    return {
        // 2.type と payload を記述する
        type: "SIGN_IN",
        payload: {
            isSignedIn: true, // signIn しているか
            uid: userState.uid, // userId
            username: userState.username
        }
    }
};
// 
export const SIGN_OUT = "SIGN_OUT";
// sign out は特にデータはないので引数はなし
export const signOutAction = () => {
    return {
        type: "SIGN_OUT",
        payload: {
            isSignedIn: false,
            uid: "",
            username: ""
        }
    }
};
```

## Reducers
> 変更を管理する状態(Store内のstate)の管理人
### 役割
Actionsからデータを受け取りStoreのstateをどう変更するのか決める
Store の状態を上書きするので指定されてない field はなくなる
**initialState**
- Store の初期状態
- アプリに必要な state をすべて記述
- export しておく
```js
const initialState = {
    users: {
        isSignedIn: false,
        uid: "",
        username: ""
    }
};
export default initialState
```
### 使い方
1. action ファイル内のモジュールを全て import (Action という名前をつける)
2. initialState を import
3. 現在の store の状態か初期状態を指定した state と action から返された値を引数にして関数を作る
4. action のタイプに応じてどの状態をどう変更するかをかく
5. 現在の store の状態を展開した後に action.payload をマージする
```js
import * as Actions from './actions'
import initialState from '../store/initialState'

// 第一引数に state(現在の store の状態が指定されてないときのために initialState をつける)
// 第二引数に action が return した値（プレーンなオブジェクトを受け取る）
export const UsersReducer = (state = initialState.users, action) => {
    // Actions の type に応じて state をどう変更するのか決める
    switch (action.type) {
        case Actions.SIGN_IN:
        return {
            // 現在存在している field を展開
            ...state,
                // isSignedIn: false,
                // uid: "",
                // username: ""

            // すでにある state を新しく書き換える
            ...action.payload
                // isSignedIn: action.payload.isSignedIn,
                // uid: action.payload.uid,
                // username: action.payload.username
        }
        default:
        return state
    }
}
```
**スプレッド構文**: 配列やオブジェクトの要素を展開する
```js
const payload = {
    uid: "0000",
    username: "shiori"
}
console.log({...payload})
// { uid: "0000", username: "shiori" }
console.log(...payload)
// uid: "0000", username: "shiori"

// Merge Objects
const state = { isSignedIn: false }
console.log({...state, ...payload})
```

## Storeとの接続
> state を管理する
1. Store と Reducers を関連づける
```js
import {
    createStore as reduxCreateStore,
    combineReducers,
} from 'redux';

// Import reducers
import {ProductsReducer} from '../products/reducers';
import {UsesReducer} from '../users/reducers';

export default function createStore() {
    return reduxCreateStore( // redux の createStore メソッドの別名
        combineReducers({ // Reducers をまとめたもの
            products: ProductsReducer,
            users: UsersReducer,
        })
    );
}
```
### `combineReducers()`とは
分割した Reducers を state のカテゴリ毎にまとめる
オブジェクトを return する (state のデータ構造)
```js
combineReducers({
    products: ProductsReducer,
    users: UsersReducer,
})

{
    products: {
        //products の state
    },
    users: {
        isSignedIn: false,
        uid: "",
        username: ""
    }
}
```

2. Redux(store) と Reactアプリ を接続する
index.js
```js
import { Provider } from 'react-redux';
import createStore from './redux/store/store';

export const store = createStore();

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>
)
```
### react-redux の Provider とは
props に store を渡す
React コンポーネント内で react-redux の connect 関数を使えるようにする
-> React と Redux を接続して App の中で store を変更・参照できるように

3. Store の状態を変更する
App() の中で
```js
const dispatch = useDispatch();
const selector = useSelector(selector: (state) => state);

console.log(selector.users);
// initialStateで定義したオブジェクトがconsoleされる

// dispatch を使って state を変更する
<button onClick={() => dispatch(signInAction( {uid: '0001', username: 'shiori'}))}>
    Sign In
</button>
```

## Routing middlewareの導入
1. react-router
React のルーティング用ライブラリ
2. connected-react-router
Redux の Store でルーティングを管理
store.js
```js
import {
    createStore as reduxCreateStore,
    combineReducers,
    applyMiddleware
} from 'redux';
import {connectRouter, routerMiddleware} from 'connected-react-router';

// 引数に ブラウザが以前どこにいたか・今どこにいるかの値を持つ history を渡す
export default function createStore(history) {
    return reduxCreateStore(
        combineReducers({
            // history の持つ情報を redux の store の router で管理
            router: connectRouter(history),
            users: UsersReducer,
        }),
        // 宣言をする
        applyMiddleware(
            routerMiddleware(history)
        )
    );
}
```
index.js
```js
import {ConnectedRouter} from 'connected-react-router';
import * as History from 'history';

const history = History.createBrowserHistory();
export const store = createStore(history);

ReactDOM.render(
    // store情報の変更
    // ブラウザURLの遷移の履歴
    <Provider store={store}>
        <ConnectedRouter history={history}>
            <App />
        </ConnectedRouter>
    </Provider>,
    document.getElementById('root'),
)
serviceWorker.unregister();
```
src/Router.jsx
```js
import {Route, Switch} from 'react-router';
import {Login, Home} from 'templates';

const Router = () => {
    return (
        <Switch>
            <Route exact path="/login" component={Logtin} />
            <Route path="/posts/:id" component={Logtin} />
            <Route exact path="(/)?" component={Home} />
        </Switch>
    )
}
export default Router;
```
- `(/)?`とすることで、スラッシュがあってもなくてもよくなる
- `:id`とすることでプログなどの記事を指定して動的に表示することもできる（この場合、`exact`はいらない
```js
<Route path="/posts/:id" component={Logtin} />
```
### templates ファイルの作成
template: URL ごとに作るファイル
src/templates/Login.jsx
```js
import {useDispatch} from 'react-redux';
// push は URL を遷移する役割を持つ
import {push} from 'connected-react-router';

const Login = () => {
    const dispatch = useDispatch();
    // 現在のストアの情報をゲット
    const selector = useSelector(state => state)

    return (
        <div>
            <h2>ログイン</h2>
            <button onClick={() => dispatch(push('/'))}>
                ログイン
            </button>
        </div>
    )
}
```



***

### View
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
- Action: typeをキーとして、stateを更新するための定義を書いで、更新するときはdispatch関数を実行することで状態更新する
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