# npm-scripts
> 直列/並列実行・監視・削除・コピーなど、タスク作成時に便利なモジュール
> package.jsonファイルに記述可能でscriptsというフィールドにshell scriptとエイリアスコマンドで指定する。
> 生産効率や品質の向上に繋がるが、タスクランナーを使わずとも、Node.jsインストール時に付属するnpm(Node Package Manager)を使用すれば、タスク処理は実現できる。

### エイリアス
> コマンド名を別のコマンド名に置き換えること。
以下のnpm-scriptsはHello world!!を表示させるコマンドのエイリアスを作成する例。
```js
{
  "scripts": {
    "hoge": "echo 'Hello world!!'"
  }
}
```
上のようにpackage.jsonファイルに記述しておけば以下のコマンドでエイリアスを実行可能になる。これがnpm-scripts。
```command
$ npm run hoge

> echo 'Hello world!!'

Hello world!!
```

## 特別扱いのスクリプト名
次の名前を持つスクリプトは特別扱い
これらは run サブコマンドを指定する必要がなく、それぞれ npm test および npm start で実行可能。
また、 test は t および tst というエイリアスを持っているため、 npm t もしくは npm tst で実行可能。
- test
テストを実行する意味合いをもっているスクリプト名。使い捨てのプロジェクトを除き、必ず定義すること。プロジェクトへのジョイン時や久しぶりにコードを触る際にまずテスト実行し、プロジェクト把握や変更の足がかりにする。
- start
プロジェクトで提供すべきものを実行するためのスクリプト名。
たとえばサーバー用のプロジェクトであればサーバーを立ち上げるための定義を、コマンドラインを提供するプロジェクトであればそのコマンドラインを実行するための定義を書く。フロントエンド開発プロジェクトではバンドル用のサーバーを立ち上げるなどの用途で利用される。関数のみを提供するなど、ライブラリーとして提供される目的のプロジェクトでは定義しなくとも良い。

## pre と post
スクリプト名の前に pre をつけたものは該当スクリプトの実行直前に実行される。
また、該当スクリプトの実行直後に実行される post プリフィクスも存在する。

test 、 pretest 、 posttestが定義されている際に test を実行すると次の順番で実行される。
1. pretest
2. test
3. posttest

## その他あると便利なスクリプト
| スクリプト名 | 目的 |
| --- | --- |
| build | ビルド |
| clean | ビルド結果の削除 |
| type-check | 型チェック |
| lint | 静的コード解析 |
| coverage | コードカバレッジ計測 |

## 複数行のスクリプトを使いたい場合
少し複雑な処理など、 1 行での定義が難しい場合は別途シェルスクリプトや JavaScript で処理を書き下すなどし、それを各種 npm-scripts に指定。

bin ディレクトリーは実行可能なパッケージを作成する際に使うものという慣習があるため、 utils や scripts ディレクトリーなどに格納。
```
/
  scripts/
    awesome.sh
  package.json
```
上述のようなファイルツリーの構造とする。
package.json の中身↓
```
{
  "scripts": {
    "awesome": "./scripts/awesome.sh"
  }
}
```

## タスク作業じに使うモジュール
ファイルのコピー・削除を行ったりブラウザを自動リロードさせるなど様々なことが可能
### コピー「cpx」
構造を維持しながらファイルをコピー
```
$ npm i -D cpx
```
例えば、階層・拡張子問わず/src内にあるすべてのファイルを/distに移動したい場合は、package.jsonへ下記のように記述して$ npm run copyを実行。
```
{
  "scripts": {
    "copy": "cpx './src/**/*' ./dist"
  }
}
```
### ディレクトリ作成「mkdirp」
ディレクトリを作成。
上で紹介した「cpx」を用いたタスクで十分だったり、何らかのタスクの実行過程で必要であれば自動作成されることが多かったりで使う場面は少ないが、それらでは該当しないようなディレクトリ作成時に使用。
```
$ npm i -D mkdirp
```
例えば、/distディレクトリを作成したい場合は、package.jsonへ下記のように記述して$ npm run mkdirを実行。
```
{
  "scripts": {
    "mkdir": "mkdirp ./dist"
  }
}
```
### 削除「rimraf」
指定したディレクトリやファイルを削除。
```
$ npm i -D rimraf
```
例えば、単純に/distを丸々削除したい場合は、package.jsonへ下記のように記述して$ npm run cleanを実行。
```
{
  "scripts": {
    "clean": "rimraf ./dist"
  }
}
```
### ディレクトリ・ファイル名を変更「rename-cli」
指定したディレクトリ・ファイル名を任意のものに変更。
```
$ npm i -D rename-cli
```
例えば、/dist/css内にあるstyle.cssをstyle.min.cssに変更したい場合は、package.jsonへ下記のように記述して$ npm run renameを実行。
```
{
  "scripts": {
    "rename": "rename ./dist/css/style.css style.min.css"
  }
}
```
### まとめて実行・直列/並列実行「npm-run-all」
自分だけが使う簡易的なものであれば&と&&で済ますこともあるが、沢山のタスクをまとめて実行させる記述を楽したいとか少しでも可読性を高くしたい場合に便利。
```
$ npm i -D npm-run-all
```
例えば、「task:A」「task:B」「task:C」という3つのタスクをまとめて実行させたいとき、&&を用いた場合はpackage.jsonへ下記のようにnpm runを複数記述するので冗長になる。
```
{
  "scripts": {
    "task:A": "echo 'task A done.'",
    "task:B": "echo 'task B done.'",
    "task:C": "echo 'task C done.'",
    "start": "npm run task:A && npm run task:B && npm run task:C"
  }
}
```
### 監視「onchange」
ファイルを監視して、追加・削除・変更など何らかの動作があったときに特定のタスクを実行。
```
$ npm i -D onchange
```
例えば、package.jsonへ下記のように記述した場合、/src内にあるhtmlに何らかの動きがあると$ npm run htmlが実行され、/src内にあるcssに何らかの動きがあると$ npm run cssが実行。
```
{
  "scripts": {
    "html": "echo changed html.",
    "css": "echo changed css.",
    "watch:html": "onchange './src/**/*.html' -- npm run html",
    "watch:css": "onchange './src/**/*.css' -- npm run css",
    "start": "npm run watch:html & npm run watch:css"
  }
}
```
### 環境変数を設定・使用する「cross-env」
異なるプラットフォームでも環境変数を設定・使用。
```
$ npm i -D cross-env
```
例えば、webpack使用時に実行コマンドによってmodeだけ変えたいときはpackage.jsonへ下記のように記述。
```
{
  "scripts": {
    "dev": "cross-env NODE_ENV=development webpack",
    "build": "cross-env NODE_ENV=production webpack"
  }
}
```
### ブラウザ確認をサポート「Browsersync」
開発開始時に表示確認用でブラウザを開いたり、ファイル変更を監視して自動的にブラウザをリロードさせることが可能。
```
$ npm i -D browser-sync
```
例えば、package.jsonへ下記のように記述して$ npm run serverを実行すると、自動的にブラウザが起動して/distをルートディレクトリとして表示し、さらにその状態で/dist内のファイルが変更されるとブラウザリロードが実行されるようになります。
```
{
  "scripts": {
    "server": "browser-sync start -s './dist' -f './dist' --port 3000 --no-notify"
  }
}
```


***
[npm-scripts でチームメンバーと共通認識を作る](https://dev.classmethod.jp/articles/be-on-the-same-page-by-using-npm-scripts/)
[npm-scripts：直列/並列実行・監視・削除・コピーなど、タスク作成時に便利なモジュール](https://www.nxworld.net/support-modules-for-npm-scripts-task.html)