---
title: CORS のエラー
slug: Web/HTTP/Guides/CORS/Errors
l10n:
  sourceCommit: 92396cf8979e107c3ac42c2b9fc382013ea1c234
---

[オリジン間リソース共有](/ja/docs/Web/HTTP/Guides/CORS) (Cross-Origin Resource Sharing) ({{Glossary("CORS")}}) は、サーバーが[同一オリジンポリシー](/ja/docs/Web/Security/Defenses/Same-origin_policy)を緩和することができる標準規格です。例えば、サイトが埋め込み可能なサービスを提供する場合、このような制約を緩和する必要があるかもしれません。このような CORS の構成の設定は必ずしも簡単ではなく、いくらか冒険的です。これらのページでは、よくある CORS のエラーメッセージと解決方法を調査します。

CORS 構成が正しく設定されていないと、ブラウザーのコンソールには `"Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at [some site]"` のようなエラーを表示して、リクエストが CORS のセキュリティ規則を侵害しているためにブロックされたことを示します。これは必ずしも設定ミスとは限りません。実際には、ユーザーのウェブアプリケーションおよびリモートの外部サービスからのリクエストが、意図的に許可されていない場合もあります。ただし、エンドポイントが使用可能である場合、成功するためにはデバッグが必要です。

## 問題の識別

CORS の構成に関する問題を理解するために、どのリクエストが、なぜ失敗したのかを調べる必要があります。そのためには以下の手順が役立つかもしれません。

1. 問題のウェブサイトやウェブアプリを実行し、[開発者ツール](https://firefox-source-docs.mozilla.org/devtools-user/index.html)を開く。
2. 失敗するトランザクションを再現してみて、[コンソール](https://firefox-source-docs.mozilla.org/devtools-user/web_console/index.html)で CORS 違反エラーメッセージが表示されるかを調べる。おそらく次のように見える。

![CORS エラーを表示している Firefox コンソール](cors-error2.png)

エラーメッセージのテキストは以下のようなものになるでしょう。

```plain
Cross-Origin Request Blocked: The Same Origin Policy disallows
reading the remote resource at https://some-url-here. (Reason:
additional information here).
```

> [!NOTE]
> セキュリティ上の理由から、 CORS リクエストで何を失敗したかについては _JavaScript コードからは特定できません_。コードから分かることは、エラーが発生したことだけです。何を失敗したかを特定するための唯一の方法は、詳細をブラウザーのコンソールで見ることです。

## CORS のエラーメッセージ

Firefox のコンソールは、 CORS のためにリクエストが失敗した場合はコンソールにメッセージを表示します。エラーテキストには、何が失敗したのかの分析が追加された "reason" の部分があります。 reason のメッセージは以下の通りです。メッセージをクリックすると、エラーをより詳細に説明し、可能な解決方法を提供する記事を開くことができます。

- [Reason: CORS disabled](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSDisabled)
- [Reason: CORS request did not succeed](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSDidNotSucceed)
- [Reason: CORS header 'Origin' cannot be added](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSOriginHeaderNotAdded)
- [Reason: CORS request external redirect not allowed](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSExternalRedirectNotAllowed)
- [Reason: CORS request not http](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSRequestNotHttp)
- [Reason: CORS header 'Access-Control-Allow-Origin' missing](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSMissingAllowOrigin)
- [Reason: CORS header 'Access-Control-Allow-Origin' does not match 'xyz'](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSAllowOriginNotMatchingOrigin)
- [Reason: Credential is not supported if the CORS header 'Access-Control-Allow-Origin' is '\*'](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSNotSupportingCredentials)
- [Reason: Did not find method in CORS header 'Access-Control-Allow-Methods'](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSMethodNotFound)
- [Reason: expected 'true' in CORS header 'Access-Control-Allow-Credentials'](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSMIssingAllowCredentials)
- [Reason: CORS preflight channel did not succeed](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSPreflightDidNotSucceed)
- [Reason: invalid token 'xyz' in CORS header 'Access-Control-Allow-Methods'](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSInvalidAllowMethod)
- [Reason: invalid token 'xyz' in CORS header 'Access-Control-Allow-Headers'](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSInvalidAllowHeader)
- [Reason: missing token 'xyz' in CORS header 'Access-Control-Allow-Headers' from CORS preflight channel](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSMissingAllowHeaderFromPreflight)
- [Reason: Multiple CORS header 'Access-Control-Allow-Origin' not allowed](/ja/docs/Web/HTTP/Guides/CORS/Errors/CORSMultipleAllowOriginNotAllowed)

## クライアント側でできること

多くの CORS エラーは、オリジン間アクセスを許可するかどうかを制御するサーバー側で解決する必要があります。一方で、クライアント側でも状況によっては次の対策を行えます。

### プリフライトの発生を避ける

サーバーがプリフライトリクエストに対応していない場合は、リクエストを単純リクエストの条件に寄せることで回避できることがあります。

- メソッドを `GET`、`HEAD`、`POST` に限定する。
- 設定するヘッダーを [CORS セーフリストリクエストヘッダー](/ja/docs/Glossary/CORS-safelisted_request_header) に限定する。
- {{HTTPHeader("Content-Type")}} は `application/x-www-form-urlencoded`、`multipart/form-data`、`text/plain` を使用する。

### `no-cors` モードを使う（opaque レスポンス）

レスポンス本文やヘッダーを JavaScript から読む必要がない場合は、 [`fetch()`](/ja/docs/Web/API/Window/fetch) の [`mode`](/ja/docs/Web/API/Request/mode) に `"no-cors"` を指定できます。

```js
fetch("https://api.example.com/log", {
  method: "POST",
  mode: "no-cors",
  body: data,
});
```

この場合のレスポンスは [`opaque`](/ja/docs/Web/API/Response/type) となり、ステータスは `0`、ヘッダーは空で、本文は JavaScript から読めません。

### プロキシサーバーを使う

アクセス先サーバーを制御できず CORS ヘッダーも設定されていない場合は、自分で管理するサーバーを経由してリクエストする方法があります。レイテンシーや運用負荷は増えますが、他の選択肢がない場合に有効です。

## 関連情報

- 用語集: {{Glossary("CORS")}}
- [CORS 入門](/ja/docs/Web/HTTP/Guides/CORS)
- [サーバー側 CORS 設定](/ja/docs/Web/HTTP/Guides/CORS)
- [CORS 有効化の画像](/ja/docs/Web/HTML/How_to/CORS_enabled_image)
- [CORS の設定属性](/ja/docs/Web/HTML/Reference/Attributes/crossorigin)
