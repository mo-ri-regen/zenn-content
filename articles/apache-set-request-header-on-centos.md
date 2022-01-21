---
title: "CentOS上でApacheのリクエストヘッダを設定する"
emoji: "🧑🏼‍🔧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [centos, apache]
published: true
---

## 設定

リクエストヘッダの値を設定するには、httpd.conf を編集します。
ヘッダ FOO に値 "bar" をセットするには、下記のように記載します。

```txt:/etc/httpd/conf/httpd.conf
<Directory>
  RequestHeader set FOO "bar"
</Directory>
```

## 参考

https://httpd.apache.org/docs/2.4/ja/mod/mod_headers.html
