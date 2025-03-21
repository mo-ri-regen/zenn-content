---
title: "英語画面設定のすすめ"
emoji: "👩‍🏫"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [english]
published: true
---

普段、著者は iPhone や Mac などは英語にして操作しています。
なぜ英語にしているかを書いていきます。

## 理由

1. サービス名の日本語訳が理解不能

AWS など一部のサービスでは日本語のままだとなにをしているのかわからないときがあります。
たとえば、API Gateway で「オーソライザー」とカタカナで書かれているのを見たとき
用語の意味がパッとわからなかったので英語にしてみました。
英語だと「Authrizers」は動詞の「authorize」の名詞になっていることから権限関連の設定をしていると推測できるようになりました。

- 日本語訳

<!-- ![日本語訳が理解不能な例(日本語画像)](/images/aws-english-recommend/authorizers_japanese.png) -->

![日本語訳が理解不能な例(日本語画像)](https://storage.googleapis.com/zenn-user-upload/f0d5dac37f72-20250116.png)
_「オーソライザー」の意味がわかりづらい_

- 英語訳

<!-- ![日本語訳が理解不能な例(英語画像)](/images/aws-english-recommend/authorizers_english.png) -->

![日本語訳が理解不能な例(英語画像)](https://storage.googleapis.com/zenn-user-upload/0c30e4073402-20250116.png)
_「Authorizers」なので権限の設定をしていると推測できる_

2. 公式ドキュメントやエラー文が英語

ドキュメントが日本語なものも増えてきていると思いますが、
リリースしたてのサービスやマニアックなサービスは
日本語訳が追いついていなくて英語のドキュメントのほうが多いと思います。
DeepL や ChatGPT など AI を活用して英訳できるようになりましたが、
英語を見ただけでアレルギー反応を起こして毎回、英訳するよりもパッと英語を見て内容を理解できたほうが学習効率がいいと思います。

3. 半角、全角の切り替えが面倒

AWS の話になりますがなにかリソースを消したい場合に
日本語入力の場合は漢字で「確認」と入力しないといけないのに対して
英語の場合は半角入力の状態で「confirm」と入力する必要があります。
AWS ではサービス名を英語で検索することがあることから半角入力状態のことが多いため
英語設定のほうが全角に切り替える必要がないという観点で楽だと思いました。

<!-- ![日本語入力](/images/aws-english-recommend/confirm_japanese.png) -->

![日本語入力](https://storage.googleapis.com/zenn-user-upload/efb975eddaa9-20250116.png)

## 最後に

Mac だとシステム設定から簡単に英語に切り替えることができるので興味をもったかたは英語設定にトライしてみましょう。

https://support.apple.com/ja-jp/guide/mac-help/mh26684/mac
