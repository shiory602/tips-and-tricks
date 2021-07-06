# Testing your Apps

## Learn the difference between Unit, Integration, and Functional tests
**Unit testing**: Testing the "units" (functions or methods of a class instance) in an application.
**Combination testing**: Ensures that multiple components of an application work together.
**Functional Testing**: Verifies that the software functionality works as specified by the upstream process or product manager.
## Unit tests
- Run fast! We are talking ms here
- Test your code in isolation
- Mock external dependencies
- Avoid database access, network requests, and the file system
- Be able to run in parallel
- Allow you to practice TDD (if you want)
## Integration tests
- Run reasonably fast. Anywhere from a few seconds to a minute
- Test how your code interacts with the framework
- May or may not mock external dependencies
- May access a local database or filesystem or network
- May or may not run in parallel
- Should NOT be used to practice TDD
[The 3 tiers of the Android test pyramid](https://medium.com/android-testing-daily/the-3-tiers-of-the-android-test-pyramid-c1211b359acd#.11kmei3e0)

## Learn how to write them with the tools

- [Jest](./Jest)

- [react-testing-library](./react-testing-library)

- [Cypress](./Cypress)

- [Enzyme](./Enzyme)

***

## ユニットテスト、インテグレーションテスト、ファンクショナルテストの違いを学ぶ
**単体テスト**：アプリケーションの中の 「ユニット (単位)」(関数またはクラスインスタンスのメソッド)をテストする
**結合テスト**：アプリケーションの複数のコンポーネントが一緒に動くことを確認する
**機能テスト**：ソフトウェアの機能が、上流工程やプロダクトマネージャーが決めた仕様通りに動作するか検証する
## ユニットテスト（単体テスト）
- 速く走れる! ここでは ms の話をしています
- コードを分離してテストする
- 外部依存のモック
- データベースへのアクセス、ネットワークへのリクエスト、ファイルシステムへのアクセスを避ける
- 並行して実行できること
- TDDを実践できる（必要に応じて
## 統合テスト
- 適度な速さで実行される。数秒から1分程度
- コードがフレームワークとどのように相互作用するかをテストする
- 外部依存関係をモックアップしてもしなくてもよい
- ローカルのデータベースやファイルシステム、ネットワークにアクセスします。
- 並列実行してもしなくてもよい
- TDDの練習には使用しないでください。

[コンポーネント（単体、ユニット）テストとは？手法などを例で紹介](https://service.shiftinc.jp/column/3636/)