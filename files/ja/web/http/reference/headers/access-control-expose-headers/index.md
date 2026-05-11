---
title: Access-Control-Expose-Headers
slug: Web/HTTP/Reference/Headers/Access-Control-Expose-Headers
original_slug: Web/HTTP/Headers/Access-Control-Expose-Headers
---

HTTP の **`Access-Control-Expose-Headers`** {{Glossary("response header", "レスポンスヘッダー")}} は、オリジン間リクエストへのレスポンスとして、ブラウザー内で実行されるスクリプトにどのレスポンスヘッダーを公開するかをサーバーが示すために使用します。

既定では、公開される {{Glossary("CORS-safelisted response header", "CORS セーフリストレスポンスヘッダー")}}は 7 つだけです。

- {{HTTPHeader("Cache-Control")}}
- {{HTTPHeader("Content-Language")}}
- {{HTTPHeader("Content-Length")}}
- {{HTTPHeader("Content-Type")}}
- {{HTTPHeader("Expires")}}
- {{HTTPHeader("Last-Modified")}}
- {{HTTPHeader("Pragma")}}

クライアントが他のヘッダーにアクセスできるようにするには、 `Access-Control-Expose-Headers` ヘッダーを使用してヘッダーを列挙する必要があります。

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">ヘッダー種別</th>
      <td>
        {{Glossary("Response header", "レスポンスヘッダー")}}
      </td>
    </tr>
    <tr>
      <th scope="row">
        {{Glossary("Forbidden request header", "禁止リクエストヘッダー")}}
      </th>
      <td>いいえ</td>
    </tr>
  </tbody>
</table>

## 構文

```http
Access-Control-Expose-Headers: [<header-name>[, <header-name>]*]
Access-Control-Expose-Headers: *
```

## ディレクティブ

- \<header-name>
  - : クライアントがレスポンスからアクセス可能になる、ゼロ個以上のカンマ区切りの[ヘッダー名](/ja/docs/Web/HTTP/Reference/Headers)です。
    これらは {{Glossary("CORS-safelisted response header", "CORS セーフリストレスポンスヘッダー")}}に追加して公開されます。
- `*` (ワイルドカード)
  - : あらゆるヘッダーを示します。
    `*` の値は、資格情報のないリクエスト（[HTTP Cookie](/ja/docs/Web/HTTP/Guides/Cookies) や HTTP 認証情報を含まないリクエスト）でのみ、特別なワイルドカード値として扱われます。
    資格情報付きのリクエストでは、リテラルなヘッダー名 `*` として扱われます。

## 例

CORS セーフリストにないレスポンスヘッダーを公開するには、次のように指定します。

```http
Access-Control-Expose-Headers: Content-Encoding
```

`Kuma-Revision` のようなカスタムヘッダーをさらに公開するには、複数のヘッダーをカンマで区切って指定できます。

```http
Access-Control-Expose-Headers: Content-Encoding, Kuma-Revision
```

資格情報のないリクエストでは、ワイルドカード値を使うこともできます。

```http
Access-Control-Expose-Headers: *
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- {{HTTPHeader("Access-Control-Allow-Headers")}}
- {{HTTPHeader("Access-Control-Allow-Origin")}}
