---
title: "SQLインジェクションについてまとめてみた"
emoji: "💉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [SQLインジェクション,フロントエンド,セキュリティ]
published: true
---

## SQL injection(インジェクション)とは

SQLインジェクションとは、開発者が予期しないSQL文を
Webサイトの入力フォームなどに埋め込むことで、不正な処理を行うことです。

また、injectionの意味を調べると、「投入、追加」 という意味があります。
なので、勘がよければ不必要なSQLを追加することで、不正な処理をさせることだと
気づくことができます。
文字だけ見ても???だと思うので、下記の例を見てください😁

### 例

```sql
SELECT * from USER where USER_NAME = '{user_name}' and PASSWORD = '{password}' 
```

USER_NAME=hogeと入力して、パスワード入力欄に下記のように入力すると

```
aaa' or '1' ='1
```

発行するSQL文は下記のようになります。
```sql
SELECT * from USER where USER_NAME = 'hoge' and PASSWORD = 'aaa' or '1' ='1'
```

後半の部分に注目すると、「'1' ='1'」からこのSQL文は必ずtrueを返すため
不正なログインができてしまいます😱
2021年5月にも、[ワクチン予約システムにSQLインジェクションをされたニュース](https://news.yahoo.co.jp/articles/afc53411dfcb63bfa62aa3f6df5a963adc304d67?page=1)がありました。
このようなことが怒らないためにもサイト運営される方は、セキュリティ対策も意識していきましょう💪
## 対策

- 入力値のチェック
半角英数字しか打てない、文字数制限があるならそれをチェックするなどの不正な値かどうかを確認するだけで、SQL文を入力しても弾かれてしまうので、防ぐことができます。

- プリペアード・ステートメントの利用
whare句など条件によって変化する部分をプレースホルダーとして登録したSQLを用意し、あとからパラメータとして割り当てます。

例
```
conn.prepareStetement("SELECT * FROM USED WHERE USER_NAME=? PASSWORD = ?")
```

元々は、プリペアード・ステートメントはSQLインジェクション対策ではなく、性能向上を目的として使われていました。
時間のかかるSQLの構文や条件の解釈を先に行い、あとでプレースホルダの変更を行います。
プリペアード・ステートメントは条件の追加など構造の変化を後から行えないため、
SQLインジェクションの防止となります。

(追記:サニタイジングはXSS対策だったので訂正)
~~- エスケープ処理を行う~~

~~「'」といった特殊な文字を普通の文字と認識するように設定します(**サニタイジング**と呼ぶ)~~
~~phpではhtmlspecialchars()という関数があるので、積極的に利用しましょう。~~
```php

echo htmlspecialchars("'", ENT_QUOTES, 'UTF-8');
// 実行結果: &#039;
```

## 参考

[SQLインジェクションのニュース](https://news.yahoo.co.jp/articles/afc53411dfcb63bfa62aa3f6df5a963adc304d67?page=1)

[プロになるためのWeb技術入門](https://gihyo.jp/book/2010/978-4-7741-4235-7)

[サニタイジング公式](https://www.php.net/manual/ja/function.htmlspecialchars.php)

[サニタイジング使い方](https://techplay.jp/column/600)