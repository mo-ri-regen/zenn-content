---
title: "Easy Cipherを解いてみた"
emoji: "⛳️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [ctf, 暗号, シーザー暗号]
published: true
---

友達に誘われて、CTF と呼ばれる[セキュリティコンテスト](https://www.seccon.jp/2021/)に参加することになったので、その練習問題を解くことにしました。

今回の問題はシーザー暗号です。

## 問題

> EBG KVVV vf n fvzcyr yrggre fhofgvghgvba pvcure gung ercynprf n yrggre jvgu ?gur yrggre KVVV yrggref nsgre vg va gur nycunorg. EBG KVVV vf na rknzcyr bs gur Pnrfne pvcure, qrirybcrq va napvrag Ebzr. Synt vf SYNTFjmtkOWFNZdjkkNH.Vafreg na haqrefpber vzzrqvngryl nsgre SYNT.

## 答え

[デコードしてくれるサイト](https://dencode.com/ja/cipher/caesar)でシーザー暗号をデコードします。13 文字シフトすると下記のようにデコード結果が現れます。(13 というのは試行錯誤した結果です。)

> ROT XIII is a simple letter substitution cipher that replaces a letter with the letter XIII letters after it in the alphabet. ROT XIII is an example of the Caesar cipher, developed in ancient Rome. Flag is ＊＊＊＊＊＊[^1]. Insert an underscore immediately after FLAG.

[^1]: 答えになるので伏せ字です。

英文を読むと

> Insert an underscore immediately after FLAG

とあるので、Flag のあとにアンダースコア入れることにだけ注意してデコード結果(＊＊＊＊＊＊)を入れます。

![正解](https://gyazo.com/aaf1226ff151caf873c40222d89e303a.md)

正解しました 🎉
