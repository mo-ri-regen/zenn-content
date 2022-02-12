---
title: "historyで簡単に過去のコマンドを実行する"
emoji: "⏱️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [linux, linuxコマンド]
published: true
---

## 用法

一つ前に実行したコマンドであれば"↑"を押せば実行できますが、
少し前に実行したコマンドとなると、"↑"を押し続けることになるので遡ることが大変です。
そのようなときに history コマンドを使うと過去に入力したコマンドを一覧で表示することができます。
どのコマンドを使ったか覚えている場合は grep で絞ると見やすくなります。

```bash
history | grep <search_word>
```

実行すると、行番号と<search_word>で絞ったコマンドが表示されるので

```bash
!<行番号>
```

を入力すると実行されます。

## 実例

"php artisan migrate" コマンドを実行したいとします。

```bash
# artisanに絞って履歴を出力する
[username@foo]$ history | grep artisan

# 実行結果
989 php artisan list
991 php artisan route:list
992 php artisan route:list
998 php artisan migrate
1012 php artisan list

# 998行目を実行
[username@foo]$ !998
```
