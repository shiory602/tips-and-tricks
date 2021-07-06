# Next.js
SEOに強いSPA開発ができる
パフォーマンスを効率化する
ルーティング（`react-router`の使用）が楽
APIの作成が簡単
TypeScriptを簡単に導入できる

**v9.0.0**
## 新しく追加された機能
- 動的ルーティング
`pages/posts/[id].js` のように動的ページのルーティングが可能に
そもそもフォルダ/ファイル構成ベースのルーティングが最高

- TypeScript標準対応
現在のフロントエンド開発では必須

- Prefetching の対応
`Link` コンポーネントの遷移先ページを事前に読み込んでおける

## SSR から SSG へ
- v9.3以前は SSR するには `getInitialProps` を使っていた
- v9.3から登場した`getServerSideProps`と`getStaticProps`の利用を推奨
- SSG(Static Site Generation)を推している
- パフォーマンスとSEOで有利だから
- CDNを用いたキャッシュと相性

 ## v9.5から登場した`Incremental Static Regeneration`を使う
ページを再生性する間隔を指定できる
初回アクセス時に生成するので負荷軽減

## v10
- Imageコンポーネントの登場
画像の最適化（WebP拡張子変換や圧縮）
画像をレスポンシブ対応（縦横比を崩さない）
- React v17のサポート
- サイトパフォーマンスの分析（Vercel利用時）
Next.jsの恩恵を最大限受けられる
Firebaseと比べてもVercelの方がいい
理由：表示速度・デプロイにかかる時間・環境構築