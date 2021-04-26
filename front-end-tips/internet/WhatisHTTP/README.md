# HTTPリクエストとHTTPレスポンスとは何ですか？

> URLにアクセスしたり、リンクをクリックする度に発生するのがリクエスト／レスポンス。（画面遷移など）
> リクエスト時は、パラメーターとしてサーバーにデータを渡すことが出来る。
> リクエストにはGET/POSTの2種類の方法がある。
> 本当に再送信されてほしくないような画面（例：注文完了画面など）や、個人情報やパスワードを入力するフォームはPOSTメソッドを使う。


Webプログラムでは、[クライアントとサーバー](https://github.com/shiory602/tips-and-tricks/tree/main/front-end-tips/internet/HowDoesTheInternetWork#%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%8D%E3%83%83%E3%83%88%E3%81%AF%E3%81%A9%E3%81%86%E3%82%84%E3%81%A3%E3%81%A6%E3%81%A4%E3%81%AA%E3%81%8C%E3%81%A3%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%81%8B)が要求と応答のやり取りを繰り返している。

ユーザーがブラウザから「このページを見せて」という【要求(リクエスト)】を行うと、
サーバーはそのページのHTMLを返してくれる。【応答(レスポンス)】

この１回分のやり取りを**１リクエスト**といい、ブラウザで画面遷移が行われる度にこのリクエストが発生している。




## HTTPリクエスト
**ブラウザ → サーバー**のやり取りでGETとPOSTがある。

### リクエストの方法
- URLに直接アクセス（アドレスバーに直接URL入力、ブックマークからアクセス）
- 画面内のリンクやボタンをクリック
- 入力フォームに入力して送信ボタンをクリック

### HTTPリクエストの構成
- リクエスト行
- ヘッダーフィールド
- ボディ（データ本体）
Webではほとんどの場合**GET**で、この場合、HTTPリクエストでは**データ本体**は送られない。


1. １行目 = **リクエスト行**
    - メソッド: `GET`もしくは`POST`
    - URL: リクエストの対象`http://~`
    - HTTPのバージョン: `HTTP/1.1`

2. ２行目以降 = **ヘッダー**(リクエストの詳細情報)

3. 空白以降 = ボディ(POSTの場合のみ)
    - 画面での入力内容

***

### GETメソッド
- クエリ文字列は大量のデータを送るのには向いていない。
- クエリ文字列はブラウザのURL欄に表示される。
- URLの末尾にパラメータをくっつけて渡す方法。
- ページの状態をブックマーク出来る


（例）
```
GET https://qiita.com HTTP/1.1
Host: qiita.com
User-Agent: curl/7.54.0
Accept: */*
```

- パラメータ付きのURL
```
http://example.com/item/modify?id=10&type=12
```
- `?`以降がパラメーター
- **【パラメータ名】=【値】**がセット
- 各パラメーターセットは`&`で区切られる

構成：
```
【URL】 http://example.com/item/modify
【パラメータ1】id 【値】10
【パラメータ2】type 【値】12
```
サーバーに対して`id`と`type`という2種類のパラメータを渡している。



### POSTメソッド
- POSTは大きめのデータを送信できる。
- 基本的に、入力フォームからのリクエストはセキュリティ上の観点からPOSTを使う。
- 入力内容はボディにありGETのようにブラウザのURLには表示されないが、解析すれば確認できるのでセキュリティ的に安全というわけではない。
- ヘッダーフィールド、ボディは省略可能。

（例）
```
POST / HTTP/1.1
Host: localhost:18888
Accept: */*
Content-Length: 46
Content-Type: application/x-www-form-urlencoded
User-Agent: curl/7.54.0

title=studying about HTTP&author=xxxxxx
```


## HTTPレスポンス 
**サーバー → ブラウザ**のやり取り

### getとpostに対するHTTPレスポンス(応答)
- そのままHTMLを返す。
- DBからデータを取得してHTMLを生成して返す。
- 要求と一緒に受け取ったデータを元に、DBに登録・更新・削除して結果を返す。

### HTTPレスポンスの構成
- レスポンス状態行
- ヘッダー
- データ本体（HTMLや画像のデータのこと）

1. １行目 = **レスポンス状態行（ステータスコード）**
    HTTPステータスコードは3桁の数字で表される。
    - プロトコルのバージョン: HTTP1.1
    - ステータスコード: 200
    - 付随するテキスト: OK
2. ２行目以降 = **ヘッダー**(レスポンスの詳細情報)
3. 空白以降 = **ボディ**(HTMLや画像等が入る)

(例)
```
HTTP/1.1 200 OK
Date: Sun, 25 Mar 2018 14:19:50 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Server: nginx
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
ETag: W/"ZGFmaWhlcmlvaGZnaWVhZ2h1aWVybGFoZmdpbGVyaA"
Cache-Control: max-age=0, private, must-revalidate
Set-Cookie: _qiita_login_session=YWZlZ3Jld2d3aW9lZ3Zkbmp2Y252ZGthamZnaWVv; domain=.qiita.com; path=/; expires=Mon, 25 Mar 2019 14:19:50 -0000; HttpOnly
X-Runtime: 0.253271
Strict-Transport-Security: max-age=2592000
X-Request-Id: 1650d346-2ed3-4bcb-9789-ed404ae13d31
Content-Security-Policy-Report-Only: default-src https: data: 'unsafe-eval' 'unsafe-inline'; report-uri https://us-central1-qiita-csp-report.cloudfunctions.net/csp-report

<!DOCTYPE html><html><head><meta charset="utf-8" /><title>Qiita</title><meta content="width=device-width,initial-scale=1,shrink-to-fit=no" name="viewport" /><meta content="#55c500" name="theme-color" /><link href="/opensearch.xml" rel="search" title="Qiita" type="application/opensearchdescription+xml" /><meta name="csrf-param" content="authenticity_token" />
#以下略
```


***


# HTTPステータスコードとは何ですか？何のために使われますか？

> HTTPステータスコードとは、WebブラウザやクローラーがURLにアクセスしようとした際、Webサーバーから返ってくるレスポンスの種類を示す3桁の数字のこと。
> この3桁の数値を**HTMLを受信する前に**受信することで、ブラウザは正しい処理ができるようになる。

## HTTPレスポンスのステータス番号

主なHTTPレスポンスのステータス番号の一覧。
- 100番台 -> 情報
- 200番台 -> 正常処理(成功)
- 300番台 -> リダイレクト関連
- 400番台 -> クライアント側のエラー
- 500番台 -> サーバー側のエラー

| ステータスコード | 説明 |
| --- | --- |
| 200 | OK: リクエストが成功しレスポンスが返されます。正常処理を表す。 |
| 301 | Moved Parmanently: 指定したリソースは移動したので、新しい場所から取得して下さい。サイトの引越しをしたときは、この値を設定。 |
| 302 | Moved Temporarily: 指定したリソースは一時的に移動したので、新しい場所から取得して下さい。一時的にサイトの場所を変える時にこの値を設定。 |
| 304 | Not Modified: 指定したファイルは変更されていないのでブラウザのキャッシュのデータを表示してください。 |
| 401 | Unauthorixed: 認証に失敗しました。 |
| 403 | Forbidden: アクセス権がありません。 |
| 404 | Not Found: リクエストしたアドレスのページがありません。 |
| 500 | Internal Server Error: スクリプトなどで内部のエラーが発生しています。 |
| 502 | Bad Gateway: ゲートウェイが無効なレスポンスを受け取りました。 |
| 503 | Service Unavailable: サービスが提供できません。Webサーバーに負荷がかかりすぎたときなどに表示されます。 |


参照: 
[MDNのHTTP レスポンスステータスコード](https://developer.mozilla.org/ja/docs/Web/HTTP/Status)
[MDNのHTTPメッセージ](https://developer.mozilla.org/ja/docs/Web/HTTP/Messages)
[MDNのHTTPの概要](https://developer.mozilla.org/ja/docs/Web/HTTP/Overview)



### 【!】ソフト404エラー
**ソフト404**とは、通常のNot Foundの404のステータスコードとは異なり、404のページのように見えるがステータスコードが**200 OK**で処理されているものである。
問題点としてソフト404エラーはステータスコードが200で返されているため、検索エンジンがクロールしてしまうことが挙げられる。
その結果、本来コンテンツがあってクロールされるべきページのクロールが遅れたり、クロールの頻度が減ってしまうなどが考えられる。

### ユーザーフレンドリーな404ページの作成
ソフト404エラーへの対策としてできること

> ユーザーに対して、探しているページが見つからないことを明確に伝えます。親しみやすく魅力的な言葉を使用します。
> 404 ページを、サイトのその他の部分と同じデザイン（ナビゲーションを含む）にします。
> 最も人気のある記事や投稿へのリンクの他、ホームページへのリンクを追加します。
> 無効なリンクを報告する方法をユーザーに提供することを検討します。
> この 404 ページがどれほどきれいにデザインされ、役に立つものであっても、Google 検索結果に表示したいとは誰も思わないでしょう。404 ページが Google や他の検索エンジンのインデックスに登録されないようにするため、存在しないページがリクエストされたときにウェブサーバーが実際の 404 HTTP ステータス コードを返すことを確認します。
> アドレス変更ツールを使用して、Google にサイトの移転を通知します。

引用元: [Google検索セントラル](https://developers.google.com/search/docs/advanced/crawling/custom-404-pages?hl=ja&visit_id=637550123061910413-2858748276&rd=1)



***


# HTTPヘッダーとは何ですか？

> HTTPリクエストヘッダやHTTPレスポンスヘッダのこと。
> ホームページを表示する際にやり取りするデータの一部で、そのデータに関する説明書きが書いてある。

書式
```
【フィールド名】:【内容】
```

## HTTPリクエストヘッダ
HTTPリクエストの２行目以降で**お願いごとやお願い元に関するあれこれ**が書かれている

[参照](https://triple-underscore.github.io/RFC7231-ja.html#section-5)
- Host: ドメイン名と任意でサーバーが開いているTCP Port番号を指定できる。
- User-Agent: ブラウザの種類やOS情報、検索エンジンクローラの名前など
- Referer: 遷移元のページ
- Cookie: ブラウザを特定するための小さなデータ。HTTPヘッダーに含まれてサーバーに送信されている。
- If-Modified-Since / If-None-Match: ブラウザに保存されているローカルキャッシュが変更されているかどうか。
- Accept: ブラウザが想定する(利用可能な)MIMEのタイプ
- Accept-Language: ブラウザが想定する(利用可能な)言語
- Accept-Encoding: ブラウザがデコードできるエンコーディング形式
- Accept-Charset: 画像の種類や、言語、文字コード等



## HTTPレスポンスヘッダ
HTTPレスポンスの２行目以降で**ステータスラインに書ききれないレスポンスの情報**が書かれている

- HTTPのバージョン: どのバージョンを使用して通信するか。
- Content-Type: 出力するデータタイプがHTMLか画像か、文字コードなどといった情報
- Server: Webサーバーの名前とバージョン等
- Expires: 取得したデータを再度サーバーに問い合わせなくてもブラウザが再利用していい期限（キャッシュの制御に使われる）
- Last-Modified / ETag
データの最終更新日時と更新チェック情報。
- Location
リクエストと違う場所からデータを取得した場合の新しい場所のURL。いわゆるリダイレクト先を示す情報。


***

### 用語集
- **パラメータ**: サーバーに受け渡すデータ(DBからのデータを判別するための`ID`や、DBに登録するための「ユーザーが入力したデータ」など)
- **クローラー**: 検索ロボット、サーチボットとも呼ばれ、インターネットにつながっているWebサイト・画像・動画などの情報を収集し、検索データベースに保管するプログラムのこと。這う（クロール：crawl）ように収集していくことからクローリングと名付けられた。
- **MIMEのタイプ**: メールやホームページのファイルつくファイル情報（`.txt`や`.html`など）



その他参照：[ITSakura](https://itsakura.com/network-http-get-post), [Qiita記事](https://qiita.com/koheiyamaguchi0203/items/5777c4653a01ae4c7b06)