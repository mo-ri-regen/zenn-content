---
title: "CLIでMySQLにログインするには"
emoji: "🎫"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [mysql, ログイン, cli]
published: true
---

## バージョン

MySQL 8.0.21

## ログイン

```bash:shell
mysql -h <localhost> -u <user_name> -P <port> -p <db_name>
```

### オプション

- -h (--host)
  MySQL が置かれている場所を指定します。
- -u (--user)
  サーバに接続するときのユーザ名を指定します
- -p (--password)
  パスワードの入力を促します。
  パスワードがないときは--skip-password を使います。
- -P (--port)
  ポート番号を指定します。

他にも多数の[オプション](https://dev.mysql.com/doc/refman/8.0/en/connection-options.html)があります。

:::message
パスワードをコマンドで指定するときは-p の直後に**スペースなし**でパスワードを入力することで指定することができます。
つまり、

```bash:shell
mysql -h <localhost> -u <user_name> -p<password> <db_name>
```

と入力します。
しかし、セキュリティの観点から[非推奨](https://dev.mysql.com/doc/refman/8.0/en/password-security-user.html)です。
:::

-p オプションを使うと下記のようにパスワードの入力が求められます。
パスワードを入力するときは何も表示されないためコマンド指定よりもセキュアになります。

```bash:shell
Enter password:
```

\<password\>を入力してログインに成功すると

```bash:shell
mysql　>
```

となります。

### ログアウト

```bash:shell
exit
```

## 参考

https://docs.oracle.com/en-us/iaas/mysql-database/doc/connecting-db-system.html
https://dev.mysql.com/doc/refman/8.0/en/connection-options.html#option_general_password
