# npm
NPMと名のつくものは実は２つあり、曖昧さを回避するために大文字と小文字で表記することで区別している。
- NPM: オンライン上のパッケージレジストリ（世界中の開発者が作ったNode.jsのパッケージが集められた場所）
- npm: Node.jsに付属しているパッケージを操作するためのCLI(コマンドラインインターフェイス)
CLIとは**全ての操作をキーボードだけで行う画面**のこと

## NPM(レジストリ)
NPM は現時点で他の言語のものを含め世界最大の**パッケージレジストリ**であり、主にブラウザ用のライブラリ、Node.js 用のライブラリが豊富に存在する。
NPM に登録されているパッケージは公式サイトでブラウジング、検索できる。

## npm (CLI)
> JavaScriptライブラリのパッケージマネージャー
> Node.jsのモジュールを管理するツール
**Node Package Manager**の略で、Node.js のパッケージを管理するための CLI である。
パッケージを作成したり、NPM 上のパッケージをローカルにインストールしたり、自分のパッケージを NPM に公開したりと、Node.js の開発に欠かせないツールである。
Node.js をインストールすると自動的に npm もインストールされる。
### yarn
似たような CLI として Facebook が開発した Yarn がある。これは npm の色々な欠点(スピードなど)を補うように作られたもの。


# パッケージ
パッケージとはプログラムがたくさん入ったディレクトリ/フォルダーのようなもので、JavaScriptでいうライブラリやフレームワークのこと。
## package.json
npmはフロントエンドで使用するパッケージのバージョン管理を行うのに用いられる。
npmでは、npmでインストールしたパッケージのバージョン情報をpackage.jsonに格納する。
このpackage.jsonからパッケージを一括でインストールすることができるため、package.jsonを一元管理することによりフロントエンド で使用するパッケージのバージョン管理を一元化することができる。
```
{
  "name": "my-package",
  "description": "my first package ever",
  "license": "MIT",
  "version": "1.0.0",
  "bin": "./cli.js",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "axios": "^0.18.0"
  },
  "devDependencies": {
    "eslint": "^5.14.1"
  }
}
```
機能的に重要なのは bin, main, dependencies, devDependencies, scripts であり、name, version, description, license などの単なるパッケージのメタデータは、パッケージを公開するつもりがないならばあまり気にする必要はない。
### dependencies & devDependencies
dependency とはそのパッケージが依存する別のパッケージであり、package.json には dependency のパッケージ名とバージョンが書かれる。
- dependencies と devDependencies の違い
dependenciesは実行に必要なパッケージ、devDependenciesは開発やテストにのみ必要なパッケージである。
機能的な違いとしては、あるパッケージ A を dependency としてインストールするときにデフォルトでは A の dependencies はインストールされるが A の devDependencies はインストールされない。

package.jsonでは次のような形式で dependency が指定される。
```
"dependencies": {
  "express": "^4.17.1",
  "request": "~2.88.0"
},
```
バージョンは.で区切られた 3 つの数字から構成されているが、これは **Semver** (Semantic Versioning) という規則に則っており、それぞれの数字に意味がある。「時間.分.秒」のように、順に細かくなっていくとイメージすればよい。
> Sematic Versioning
> 1. Major: APIの変更・使い側のコードを修正する必要あり
> 2. Minor: 新機能の追加
> 3. Patch: バグ修正
dependencies または devDependencies でバージョンを指定する時、
> - キャレット^: Major は一致し Minor と Patch は指定されたもの以上
> - チルダ~: Major と Minor は一致し Patch は指定されたもの以上
> (例)^4.17.1は4.17.10や4.20.0にマッチするが4.16.8や3.20.4にはマッチしない。
> ~2.88.0は2.88.5にマッチするが2.90.3にはマッチしない。
> 逆に ^ も ~ もつけなければ ちょうどそのバージョンにのみマッチする。

後述の package-lock.json ファイルが存在せず、dependency がローカルにインストールされていない状態で npm install を実行すると、上記のルールにしたがい、package.json に指定されたバージョンにマッチする中で最も新しいバージョンがインストールされる。
※バージョンを固定したいときは後述のpackage-lock.jsonを使えばよいため、わざわざキャレットやチルダを外す必要はない。

### scripts
scripts は簡単に言えばコマンドのエイリアスであり、任意のコマンド(i.e. コマンドラインのコマンド)に名前をつけることができる。
```
  "scripts": {
    "start": "node index.js",
    "lint": "eslint"
  },
```
ここに記載された script は`npm run <name>`で実行できる。

**特別扱いされる名前**
- start: 普通プログラムを実行するコマンドを指定し、npm startで実行できる。
- test: テストを実行するコマンドを普通指定し、npm testで実行できる。
- script 名の先頭にpre: ついてない名前の script が実行される前に自動的に実行される。
- script 名の先頭にpost: 元の名前の script の後に実行される。

### main
main はそのパッケージを外からインポートするときにどの JavaScript ファイルが入り口であるかを指定するものである。
誰かのパッケージを外から使うときに、そのパッケージをインポートするとは具体的にどのファイルをインポートするということなのかを確認するときに見ればよい。自分のパッケージのpackage.jsonの main は、そのパッケージを NPM で公開しない限り重要ではない。

### bin
これも、パッケージを外から使うときにのみ重要になる項目である。パッケージ A の package.json の bin に何らかの実行可能ファイルが指定されていると、パッケージ A をインストールすればそれを CLI として実行できるようになる。

### dependency の編集
すでにnpm installですべての dependency をインストールした状態で、dependency を追加・削除・アップデートしたいときは普通直接package.jsonを編集せず、npm を通じて行う。
npm コマンドで dependency を変更すると自動的にpackage.jsonにも反映される。
もしpackage.jsonを直接編集した場合は再度npm installを実行してnode_modules内のファイルを更新する必要がある。

※ npm v4 以下では dependencies として追加するときに--saveを指定しないとpackage.jsonに反映されない。


## インストールの種類
npmではパッケージをインストールする方法が、グローバルインストールとローカルインストールの二種類存在する。
### グローバルインストール
npmのルート配下にあるnode_modulesにパッケージがインストールされる。
Node.jsインストールじにNode.jsの実行モジュールのインストール先にパスが通されているため、グローバルインストールされたパッケージを全てのプロジェクトで使用することができる。
### ローカルインストール
プロジェクトのルート配下にあるnode_modulesにパッケージがインストールされる。ローカルインストールされたパッケージは対象のプロジェクトのみで使用することができる。


# npmの使い方
Node.jsをインストールすると同時にnpmもインストールされる

## バージョン確認
npmが動作しているか確認する
```
npm --version
```
npm: npmを実行することを宣言
--version: バージョン情報を表示することを指定
## パッケージのインストール
```
npm install パッケージ名
```
### インストール済みパッケージの確認
```
npm list -g
```
list: インストール済みのパッケージを表示するコマンド
-g: 使用しているコンピュータ内の全てのパッケージを表示
## その他のnpmコマンド
| コマンド | 意味 |
| npm i <package> | パッケージをインストール |
| npm i -g <package> | パッケージをグローバルにインストール |
| npm un <package> | パッケージをアンインストール |
| npm up | パッケージをアップデート |
| npm t | テストを行う |
| npm --version | npmを最新にする |
| npm help | ヘルプ機能を使う |



***
[npm公式サイト](https://www.npmjs.com/)
[【初心者向け】NPMとpackage.jsonを概念的に理解する](https://qiita.com/righteous/items/e5448cb2e7e11ab7d477)