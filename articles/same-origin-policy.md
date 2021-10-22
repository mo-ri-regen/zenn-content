---
title: "同一オリジンポリシーについて"
emoji: "🔐"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [js, セキュリティ]
published: true
---

## 定義

JSなどのクライアントスクリプトからサイトをまたがったアクセスを禁止するセキュリティ上の制限のことをいいます。たとえばiframeを使ってiframeの内側のHTMLを閲覧することを制限することができます。この制限をすることでパスワードなどの秘密情報の取得をさせないようにします。

## 同一オリジンである条件

- URLのホスト(FQDN; Fully Qualified Domain Name)が一致していること
- スキーム(プロトコル)が一致していること
- ポート番号が一致していること

### 例

http://store.company.com/dir/page.html に対して下記の例で同一オリジンであるか確認してい
きます。(⭕️が同一オリジン)

ここで、"http://store.company.com/dir/page.html"は
ホストは"store.company.com"
スキームはhttp
ポート番号は80^[ポート番号の80は省略されます]
だということがわかります。

|  URL  |  結果  |理由|
| ---- | ---- |--------|
|  http://store.company.com/dir2/other.html  |  ⭕️  ||
|  http://store.company.com/dir/inner/another.html  |  ⭕️  ||
|  https://store.company.com/page.html  |  ❌  |プロトコルが異なる|
|  http://store.company.com:81/dir/page.html  |  ❌  |ポート番号が異なる|
| http://news.company.com/dir/page.html  |  ❌  |ホストが異なる|

:::message alert
同一オリジンポリシーが守られていても、アプリケーションに脆弱性があると攻撃を受けることがあります。たとえばXSS攻撃をされるときに同一オリジンポリシーが守られていると、iframeの外側にあるJSで内側(別ホスト)をアクセスするとアクセス拒否されます。しかし、内側にJSを送り込んで実行することができた場合、同一オリジンポリシーの制約を受けないので攻撃することができます。
:::

:::details CORS(Cross-Origin Resource Sharing)について
同一オリジンポリシーが守られていなくても、サイト間で通信するときに相手側の許可があれば同一オリジンでなくても通信ができる仕様のことを**CORS**といいます。
本では、XMLHttpRequestのケースで説明されてます。
:::

## 参考

[同一オリジンポリシー(MDN)](https://developer.mozilla.org/ja/docs/Web/Security/Same-origin_policy)
[体系的に学ぶ 安全なWebアプリケーションの作り方 第2版](https://www.sbcr.jp/product/4797393163/)