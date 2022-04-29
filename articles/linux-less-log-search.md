---
title: "tailより便利なコマンドlessでログ監視する"
emoji: "👀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [linuxコマンド, cli]
published: true
---

前回、[tail を使ったログ監視方法](https://zenn.dev/mo_ri_regen/articles/linux-tail-log-search)を書きましたが、今回は tail を使わずにログを監視する方法について書きます。
その方法は less に F オプションを指定することです。

```bash
less +F file_name
```

tail とは違い less でログの監視を行うと検索がすぐに行えて便利です。
具体的には、下記のような画面のときに Ctrl+C でログの監視を停止すると less のときと同様、「/{検索したい文字}」で検索を行えます。

```bash
<ログ>
Waiting dor data...(interrupt to abort)
```

終了したいときは「:q」を押します。
