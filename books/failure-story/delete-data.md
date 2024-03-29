---
title: "データベースから必要以上のデータを削除してしまった話"
free: true
---

## 環境

- MySQL
- CentOS

## 経緯

2022 年 4 月 14 日に手動でバッチ実行できるかテストをするためにステージング環境でデータを削除する必要がありました。
また、そのデータは外部キーで紐づいていたため、1 テーブルだけを削除するのではなく SQL を使って複数のテーブルからデータを削除する必要がありました。

データ削除をする SQL 文はすでにあったのでそれを実行すればよいと考えていたのですが、その SQL 文は日付の指定がされていませんでした。対象データかどうかの確認はしっかりしたのですが、日付のところまでは頭が回っておらず 1 日分だけ削除すればよいのに対象データの対象データの全データが消えてしまいました。
https://twitter.com/mo_ri_regen/status/1514542031766691845

削除する前にバックアップとして mysqldump コマンドを実行していたのですが、実行する場所を間違っていたせいでエラーが発生していました。そのエラーにも気づかずに削除する SQL 文を実行したためバックアップも取れていませんでした。

## 原因と解決策

### 確認漏れ

確認するときに SQL 文だけをみて判断していましたが、どのデータを削除するか WHERE 文に記載してある箇所を SELECT で確認していれば日付指定が漏れていることに気づけたのではないかと思います。

### バックアップミス

mysqldump コマンドを実行したあとにエラーに気づけていればミスをしたとしても元に戻すことができました。
なので、コマンドを実行した後は実行結果の文章をよく確認する重要性を再認識しました。
