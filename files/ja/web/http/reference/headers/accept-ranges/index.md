---
title: Accept-Ranges
slug: Web/HTTP/Reference/Headers/Accept-Ranges
original_slug: Web/HTTP/Headers/Accept-Ranges
---

HTTP の **`Accept-Ranges`** {{Glossary("response header", "レスポンスヘッダー")}} は、サーバーが[範囲リクエスト](/ja/docs/Web/HTTP/Guides/Range_requests)に対応していることを示すために使用されます。このフィールドの値は、範囲の定義に使用できる単位を示します。

例えば、レスポンスに `Accept-Ranges` ヘッダーがある場合、クライアントは転送全体を最初からやり直す代わりに、中断されたダウンロードの再開を試みることができます。

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

```
Accept-Ranges: <range-unit>
Accept-Ranges: none
```

## ディレクティブ

- `<range-unit>`
  - : サーバーが対応している範囲の単位を定義します。 `bytes` は {{RFC("7233")}} で公式に定義されている唯一の範囲の単位ですが、追加の範囲の単位が [HTTP Range Unit Registry](https://www.iana.org/assignments/http-parameters/http-parameters.xhtml#range-units) に登録されている可能性があります。
- `none`
  - : 範囲の単位に対応していないことを示します。
    これはヘッダー自体を省略した場合と等価で、現在はほとんど使用されません。
    過去には、サーバーが範囲リクエストに対応していない場合に、ダウンロードマネージャーの一時停止ボタンを無効化する目的で使われることがありました。

## 例

```
Accept-Ranges: bytes
```

## 仕様書

| 仕様書                                  | 題名                                                   |
| --------------------------------------- | ------------------------------------------------------ |
| {{RFC("7233", "Accept-Ranges", "2.3")}} | Hypertext Transfer Protocol (HTTP/1.1): Range Requests |

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [HTTP 範囲リクエスト](/ja/docs/Web/HTTP/Guides/Range_requests)
- [HTTP 条件付きリクエスト](/ja/docs/Web/HTTP/Guides/Conditional_requests)
- {{HTTPHeader("Range")}}, {{HTTPHeader("If-Range")}} リクエストヘッダー
- [IANA HTTP Range Unit Registry](https://www.iana.org/assignments/http-parameters/http-parameters.xhtml#range-units)
