# yarn
yarnはパッケージマネージャである。node.jsに付属されているnpmとほぼ同様の機能を持っていて、npmの代替としてyarnを使用することがほとんどである。
- 並行処理でのインストールによってnpmよりも高速にパッケージをインストールできる。
- npm の多くの機能を相互運用することができるように作られていて、既存プロジェクトの package.json をそのまま利用できるため、移行も容易である。
- node_modules管理方法が、npmは階層化されているのに対し、yarnはフラットなので、インストールに重複がない分の容量が減って軽くなる。

## yarnの導入

### インストール
Homebrewを使う方法とnpmを使う方法がある。（前者推奨）
```
brew install yarn
```
### プロジェクトの準備
package.jsonを作成する
```
cd path/to/directory
yarn init
```

### モジュールの追加
パッケージをインストールするにはaddコマンドを使用する。
- -S: package.jsonのdependenciesとして登録
- -D: devdependenciesとして登録
基本的に開発時のみに使用されるものはdevdependenciesに登録される。
```
yarn add react react-dom -S
npm install react react-dom -D
```

### モジュールの削除
削除するときはremoveコマンドを使う。
```
yarn remove react react-dom -S
```





***
[yarn公式](https://classic.yarnpkg.com/en/)