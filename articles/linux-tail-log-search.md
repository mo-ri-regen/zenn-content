---
title: "tailを使ってログ監視する方法"
emoji: "👀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [linuxコマンド, cli]
published: true
---

tail コマンドを使うとファイルの中身を表示できます。

デフォルトでは最終行から 10 行分の内容が表示され、n オプションを指定すると行数の指定ができます。
f(follow)オプションを指定することでファイルの行が追加されるとリアルタイムで表示されるためログを監視することができます。

```bash
tail -f file_name
```

Ctrl+c で終了します。
