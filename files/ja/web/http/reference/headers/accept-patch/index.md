---
title: Accept-Patch
slug: Web/HTTP/Reference/Headers/Accept-Patch
original_slug: Web/HTTP/Headers/Accept-Patch
l10n:
  sourceCommit: 36001a269f4d7b2b3ac6de79e942a5f849bb87d8
---

**`Accept-Patch`** は HTTP の {{Glossary("response header", "レスポンスヘッダー")}} で、サーバーが {{HTTPMethod("PATCH")}} リクエストで解釈できる[メディアタイプ](/ja/docs/Web/HTTP/Guides/MIME_types)を示します。

例えば、サポートされていないメディアタイプの `PATCH` リクエストを受信したサーバーは、{{HTTPStatus("415", "415 Unsupported Media Type")}} と、1 つ以上のサポート済みメディアタイプを列挙した `Accept-Patch` ヘッダーを返すことができます。

このヘッダーは、`PATCH` メソッドに対応したリソースへの {{HTTPMethod("OPTIONS")}} リクエストで示されるべきです。また、任意のリクエストメソッドへのレスポンスに `Accept-Patch` が含まれている場合は、対象リソースで `PATCH` が許可されていることを暗黙的に意味します。

> [!NOTE]
>
> - IANA レジストリーが[公式なコンテンツエンコーディングの完全なリスト](https://www.iana.org/assignments/http-parameters/http-parameters.xml#http-parameters-1)を管理しています。
> - `bzip` および `bzip2` エンコーディングは標準ではありませんが、特に過去の実装に対応するために使用されることがあります。

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">ヘッダー種別</th>
      <td>{{Glossary("Response header", "レスポンスヘッダー")}}</td>
    </tr>
  </tbody>
</table>

## 構文

```http
Accept-Patch: <media-type>/<subtype>
Accept-Patch: <media-type>/*
Accept-Patch: */*

// カンマ区切りのメディアタイプ一覧
Accept-Patch: <media-type>/<subtype>, <media-type>/<subtype>
```

## ディレクティブ

- `<media-type>/<subtype>`
  - : `text/html` のような単一で明確な [MIME タイプ](/ja/docs/Web/HTTP/Guides/MIME_types)です。
- `<media-type>/*`
  - : サブタイプを省略した MIME タイプです。
    例えば、`image/*` は `image/png`、`image/svg`、`image/gif` などの画像タイプに対応します。
- `*/*`
  - : 任意のメディアタイプです。

## 例

```http
Accept-Patch: application/json
Accept-Patch: application/json, text/plain
Accept-Patch: text/plain;charset=utf-8
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

ブラウザーの互換性はこのヘッダーには関係ありません（ヘッダーはサーバーから送られ、仕様書ではクライアントの動作を定義していません）。

## 関連情報

- {{HTTPHeader("Accept-Post")}}
- {{HTTPStatus("415", "415 Unsupported Media Type")}}
- {{HTTPMethod("PATCH")}} リクエストメソッド
