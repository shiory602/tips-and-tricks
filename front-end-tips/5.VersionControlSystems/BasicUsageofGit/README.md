# What are they and why you should use one

## Git
> A distributed version control system.
> General term for Git clients and Git servers
- Git client: The CUI for Git
- Git server: A server that acts as a shared repository server (used remotely), mainly by accepting push requests from outside.

In a development environment where a team is working on a single program, it is common for multiple people to make changes to the same file.
This is a mechanism to avoid conflicts between changes, which can cause bugs and make it difficult to revert to the original state.

### Gitbash
A custom terminal software that allows you to use git conveniently on windows.
### bash.
It is often used on Unix and Linux.

GitBash is automatically installed when you install Git for Windows.

**GitBash is automatically installed when you install Git for Windows, while Mac and Linux** come with Bash functionality as a standard feature, such as the **Terminal**.


### Version Control System
A version control system is a system that keeps track of who, when, and what changes have been made to source code as "versions".
A version control system records changes made to files on a computer and manages the record history.
Each worker makes changes as a local repository by copying the data on the net, which is called a remote repository.
> The advantage is that you can track changes to the source code at any time and easily revert to the original version if a problem is found.

### Differences between Git and other version control systems
- Version control systems other than Git allow you to make changes directly in a "master repository" on a shared server.
- On the other hand, with Git, you create a "local repository" on each computer, which is a copy of the master repository.
The local repository has the advantage of preventing half-baked changes from entering the master repository.

### Difference between Git and GitHub
GitHub is a **web service** built on the same mechanism of Git.
By using GitHub, anyone can store and publish source code and other data for free.
It is also possible to create a private repository that only any person can access.

## Basic Git terminology
| Terminology | Meaning
| --- | --- | Repository
| Repository | A place to store and manage source files and other data.
| remote repository | a repository shared with team members on a server
| Local repository | A repository managed by each team member by copying the master repository.
| Clone | Copy (duplicate) a repository
| Fork | Clone another developer's repository on GitHub.
| Init | Create a new repository.
| pull | pull data from a master repository into a local repository
| Push | Add changes from the local repository to the master repository.
| commit | Record work on a file or directory in the local repository.
| worktree | directory in which the user is working
| merge | merge changes from different repositories
| conflicts | errors that cause changes to occur in the same place in the same file at the same time

### branch
> The ability to create a branch repository by copying the master repository.
By using the branch function, even large scale changes can be developed without affecting the master repository.
Also, if you create multiple branch repositories, you can share development among multiple people.


## What you can do with Git
- Keep track of changes to files: no need to write them down on your own.
- Easily revert to the previous version of a file: Easily revert any file to the version you want with a single command.
- Manage everything you need for your project: Manage any file.
- Share with your team: Share information about who changed what.

## Git Steps
1. use a git hosting service to create a repository (project)
2. copy (clone) the repository to your local machine (your computer)
3. add files to your local repository and "commit" (update) your changes
4. push your changes to your master branch
5. committing changes to a file using the git hosting tool
6. pull changes locally
7. creating a new branch (version) and committing changes
8. opening a pull request (suggesting a change to your master branch)
9. merging your current branch into your master branch Translated with www.DeepL.com/Translator (free version)

***


# What are they and why you should use one

## Git
> 分散バージョン管理システムのこと
> Git クライアントと Git サーバの総称
- Git クライアント： Git の CUI
- Git サーバ： 主に外部からの push リクエストを受け付けたりして共有リポジトリサーバとして振る舞う（リモートで利用される）

チームで１つのプログラムを作り上げていく開発の現場で同じファイルに対して複数人が変更を入れることがよくある。
その際、変更同士が　ぶつかってバグを起こしたり、元の状態に戻すのが困難になるのを防ぐための仕組み。

### Gitbash
windows上でgitを便利に使えるようにカスタムして提供されているターミナルソフト
※bash：
命令を画面に打ち込むとコンピュータが命令に従いファイルの操作やファイルの編集、削除といった操作ができるソフトウェア。UnixやLinuxでよく使われる。

GitBashはGit for Windowsをインストールすることで自動的にインストールされる。

**MacやLinux**はBashの機能が**ターミナル**といった名前などで標準的に搭載されている。


### バージョン管理システム
「誰が・いつ・どのような変更をソースコードに加えたか」という情報を、「バージョン」として記録しておくもの。
コンピュータ上のファイルなどに発生した変更を記録し、その記録履歴を管理する。
リモートリポジトリと呼ばれるネット上のデータをコピーして、各作業者がローカルリポジトリとして変更を加える。
> メリットは、ソースコードの変更状況をいつでも把握できるかつ、問題が見つかっても簡単に元のバージョンへと戻せること。

### Gitと他のバージョン管理システムとの違い
- Git以外のバージョン管理システムでは、共有サーバー上の「マスターリポジトリ」を直接変更する。
- 一方、Gitの場合はマスターリポジトリをコピーして作った「ローカルリポジトリ」を各々のパソコン内に作成する。
ローカルリポジトリというワンクッションを挟むことで、中途半端な変更がマスターリポジトリに入るのを防ぐメリットがある。

### GitとGitHubの違い
GitHubは、Gitの仕組みをそのまま利用して作られた**Webサービス**です。
GitHubを使うことで、誰でも無料でソースコードなどのデータを保存・公開できる。
また、任意の人だけアクセスできるプライベートなリポジトリを作ることも可能。

## Gitの基本用語
| 用語 | 意味 |
| --- | --- |
| リポジトリ | ソースファイルなどを管理するための格納場所 |
| リモートリポジトリ | チームメンバーとサーバー上で共有するリポジトリ |
| ローカルリポジトリ | マスターリポジトリをコピーして各担当者が管理するリポジトリ |
| クローン | リポジトリをコピー（複製）する |
| フォーク | 他の開発者のリポジトリをGitHub上でクローンする |
| イニット | リポジトリを新規作成する |
| プル | マスターリポジトリのデータをローカルリポジトリに取り込む |
| プッシュ | ローカルリポジトリの変更内容をマスターリポジトリに加える |
| コミット | ファイルやディレクトリの作業をローカルリポジトリに記録 |
| ワークツリー | ユーザーが作業中のディレクトリ |
| マージ | 異なるリポジトリの変更内容を統合 |
| コンフリクト | 同じファイルの同一箇所で同時に変更が起こってしまうエラー |

### branch
> マスターリポジトリをコピーして分岐リポジトリを作成する機能のこと
ブランチ機能を使うことで、規模の大きい変更でもマスターリポジトリに影響を与えずに開発できる。
また、複数の分岐リポジトリを作成すれば複数人で分担しながらの開発も可能。


## Gitを使ってできること
- ファイルの変更履歴を管理できる：各自で変更履歴をメモしておく必要がない
- 簡単に変更前のファイルに戻せる：コマンド１つで任意のファイルを好きなバージョンへと簡単に戻せる
- プロジェクトに必要なあらゆるものを管理できる：ファイルならなんでも管理できる
- チーム内で共有できる：誰が何を変更したのかの情報共有ができる

## Gitの手順
1. gitホスティングサービスを使ってレポジトリ（プロジェクト）を作成する
2. ローカル（自分のコンピュータ）にレポジトリをコピー（クローン）するmachine
3. ローカルレポジトリにファイルを追加して変更を「コミット」（更新）する
4. 変更をマスターブランチにプッシュする
5. gitホスティングツールを使ってファイルの変更をコミットをする
6. ローカルに変更をプルする
7. 新しくブランチ（バージョン）を作成して変更をコミットする
8. プルリクエストを開く（マスターブランチに変更を提案する
9. マスターブランチに現在のブランチをマージする

***

[【Git入門】基礎知識から使い方、学習法までわかりやすく解説](https://www.sejuku.net/blog/72524)
[いまさらだけどGitを基本から分かりやすくまとめてみた](https://qiita.com/gold-kou/items/7f6a3b46e2781b0dd4a0)