# Repo Hosting Services
Gitのホスティングサービスには色々種類があり、企業によって使用するサービスは異なる
- [GitHub](https://github.com/): 最大手で容量制限もないがプライベートレポジトリは有料のみ
- [Bitbucket](https://bitbucket.org/): 全て無料だがコミットユーザーに制限あり
- [GitLab](https://about.gitlab.com/): GitHubのクローン
- [CloudForge](http://www.cloudforge.com/): リポジトリ制限なし有料
- [tracpath](https://tracpath.com/): 日本語によるサポートと契約を受けることができる

# Learn to use GitHub
## 新規レポジトリの作成
全く新しくレポジトリを作って登録する方法
### GitHubに登録する
登録がまだの場合はSign upする
### リモートリポジトリを作成する
- Repository name: リポジトリ名
- Description: リポジトリの説明
- Publicを選択（Privateは有料会員のみのサービス）
- README: READMEファイルを作成する場合のみチェック
### ローカルリポジトリを作成する
`mkdir`でディレクトリ（フォルダ）を作成し、`cd`でフォルダ内に移動
```
mkdir sample
cd sample
```
`git init`コマンドでリポジトリを作成
```
git init
```
これで空のローカルレポジトリの作成が完了
### ファイルを追加・削除する
作ったディレクトリに以下のファイルを作成
```
touch sample1.txt
touch sample2.txt
```
作成したファイルを`git add`でGitのインデックスに追加する
まとめて追加するときは`git add .`を使う
```
git add ファイル名
```
> 追加されたか確認するときは`git status`を使う
ファイルが追加されたら`git command`でGitにコミット（登録）する
```
git commit -m "残したいメッセージをここに書く"
```
### レポジトリを更新する
初めての送信の時は`git remote add origin GitHubで取得したURL`でリモートリポジトリへの追加作業を行う
この作業は２回目以降は必要ない
```
git remote add origin https://github.com/ユーザーID/リポジトリ名
```
続いて`git push`で更新内容を送信する
```
git push origin main
```
## 既存レポジトリの更新をする方法
ファイルを編集して更新
### 追加・登録を行う
```
git add .
git commit -m "ファイルの更新確認"
```
編集内容を登録したら送信する
```
git push
```
## プルリクエストを送る方法
誰かに自分のコードを見てもらうときに使う
### 新しいブランチを作成する
ブランチを切り替える時に使う`git checkout`に`-b`をつけることで新しくブランチを作成しそこに切り替える
新しくブランチを作成したら必ず`git push`を行うこと
```
git checkout -b 新しくつくるブランチ名 origin/main
git push -u origin 新しくつくるブランチ名
```
### ブランチを確認する
現在作成済みのブランチを確認する時は`git branch`を使う
`git branch --all`でローカルとリモート全てのブランチを確認できる
```
git branch
```
### プルリクエストを行う
プルリクエスト（PR）はGitHub上で新しく作ったブランチにデータを登録した後行う
リクエストした相手に確認をしてもらった後は承認をえてブランチを削除する
編集・更新はローカルで行い、プルリクエストの動作はリモートで行う
### ブランチの削除
全ての更新が終了したら作成したブランチをmainから切り離す動作を行う
この動作を行う前に`git branch --all`をすると全てのブランチが見れるが、削除動作後にもう一度見るとPRで使っていたブランチがリモート上から消えていることが確認できる
```
git fetch --prune
```
- fetch: リモートからデータをもらう
- --prune: データを切り離す（削除）




[Gitの基本的な使い方とは？初心者向けにわかりやすく解説](https://www.sejuku.net/blog/74318)