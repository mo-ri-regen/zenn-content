---
title: "例を通してCSPの理解を深める"
emoji: "💂‍♀️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [csp, セキュリティ, security]
published: true
---

## コンテンツセキュリティポリシー (CSP)とは

[XSS 攻撃](https://zenn.dev/mo_ri_regen/articles/cross-site-scripting)の軽減やデータインジェクション攻撃の軽減をするために追加できるセキュリティレイヤのことです。
web サーバのレスポンスヘッダに"Content-Security-Policy"を設定する必要があります。
設定をすることで、どのアクセスを許可するかといったことやアラートの報告先を指定することができます。

## 例

```
Content-Security-Policy: default-src 'self'; img-src \*; media-src media1.com media2.com; script-src userscripts.example.com
```

> default-src 'self'

すべてのコンテンツをサイト自身のドメイン(サブドメインを除く)から取得させたいということを表します。

> img-src \*

任意のドメインからの画像の読み込みを許可します。

> media-src media1.com media2.com;

音声や動画などのメディアは media1.com media2.com のみ許可されます。

> script-src userscripts.example.com

実行可能なスクリプトは userscripts.example.com のみです。

## 違反報告

```
Content-Security-Policy: default-src 'self'; report-uri http://reportcollector.example.com/collector.cgi
```

report-uri で指定した URI に違反内容を報告します。

## サーバ設定

Apache では VirtualHost の httpd.conf または.htaccess ファイルに下記のように設定します。

```txt:/etc/httpd/conf/httpd.conf
Header set Content-Security-Policy "default-src 'self';"
```

## サポートブラウザ

IE を除くブラウザでサポートされています。

## 参考

https://developer.mozilla.org/ja/docs/Web/HTTP/CSP
https://content-security-policy.com/
