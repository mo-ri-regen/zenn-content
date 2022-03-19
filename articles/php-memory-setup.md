---
title: "コマンド実行したらメモリ不足というエラーが出た話"
emoji: "🥡"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [php, laravel, メモリ]
published: true
---

## エラー内容

Laravel で自作したコマンド[^1]をステージング環境で実行したらエラーが発生してしまいました。

[^1]: 私が作ったコマンドではないです

```bash
PHP Fatal error: Allowed memory size of 134235547 bytes exhausted
(tried to allocate 4096 bytes) in /home/httpd/foo/bar/Query.php
on line 30
```

## 解決策

デフォルトのメモリの設定が 128 メガバイトです。そのため、メモリが足りずにエラーが出ていました。
なので、コマンドを実行している関数の冒頭に ini_set 関数でメモリを設定をすると実行ができました。

```php
ini_set("memory_limit", "1024M");
```

## 反省

開発環境で実行したときは特に問題が起きず、コマンドの処理時間は 1 時間程度でした。
なので、ステージング環境で実行するときも 1 時間後に見ればいいかなと考えていたのですぐにエラーに気づきませんでした。
長時間かかる場合はログを定期的に見て状況を確認する必要性を感じました。

開発環境でエラーが出なかった原因は、どうやら開発環境とステージング環境でメモリの設定が違っていたからでした。

## 参考

https://www.php.net/manual/ja/function.ini-set.php

https://www.php.net/manual/ja/ini.core.php#ini.memory-limit
