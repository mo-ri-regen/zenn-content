---
title: "PWANight2021に参加してみた感想"
emoji: "👽"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [PWA, フロントエンド,PWANight]
published: true
---

[conpass](https://pwanight.connpass.com/event/204759/)にPWAのイベントの募集があったので参加してみました。

## 雰囲気

すべてオンラインで行われていて、oVice上で行われました。
trackA~trackCまでYoutube上でライブ配信という形で放送されていて
興味のあるところへ参加するという形式でした。([stream](https://streamyard.com/)というものを使っていたらしいです。)
trackCではワークショップとして「国産のヘッドレスCMSであるmicroCMSとNuxt.jsを使ってJamStackのブログを作る」ということを行ってました。
~~(Next.jsだったら参加してたかも)~~

## 著者のスキル

- Nextjs,Reactについて2021年2月くらいから勉強し始めた
- PWAについて聞いたことあるけどよくわかっていない

## 参加したconference

### サンプルを通して学ぶPWA開発(PWA Night for Beginners)

初心者向けのconference。
PWAとはWebアプリとネイティブアプリのいいとこ取りを目指したものです。
まずは既存のWebアプリをPWA対応してみるところから始める、
PWAのチェックリストを無理して全部満たさなくていいといったことを言ってました。
[LightHouse](https://developers.google.com/web/ilt/pwa/lighthouse-pwa-analysis-tool)を使ってPWA対応ができているかチェックしてましたが、
headタグの追加(ios)とmanifest.jsonファイル追加(Android)するだけで達成できてて
簡単そうだなとみてて思いました。

### PWAとクラウドゲーミング、そして共に歩むOOPartsのこれから。

AmazonやMicrosoftもクラウドゲーミングに力を入れているということが紹介されてました。
[Onesignal](https://onesignal.com/)というのを使うと簡単にpush通知を埋め込めるそうです。
また、OOPartsはNextjsに移行しようとしていて苦労話が聞けました。
その他、プレステのコントローラを使ってPCを操作していました。
「◯」ボタンを押すとEnterと同じ挙動を行っていたが、将来的には左スティックを使ってカーソル移動などを行いたいそうです。

PWAの課題として、

- iosとAndroidの差が大きい
- PWAの認知度が低い
- iosのアプリはまだ表現しづらい

などがあるそうです。

### PWAで覗き見るSSI（自己主権型アイデンティティ）の世界

SSI(Self Sovereign Identity)とは、自分のIDは自分で管理するという概念のことです。
たとえば、プロフィールにLINEのIDやTwitterのアカウント名を載せることがあると思いますが、
それらはLINEやTwitterといったプラットフォームに依存しているので、そのようなプラットフォームに依存せずに自分のことを証明する技術のことのようです。
ブロックチェーンを使ったDID(分散型ID)やVC(Vertifable Credential)といったものがあるそうです。(あまり理解できてなかった😅)
技術が先端すぎて、ググってもドキュメントすら出てこずにソースコードを読み解くしかなかったらしく、苦労したそうです。
作りながら、勉強していったということで登壇者のチャレンジする意欲がすごいなと思いました。

## 感想

総合すると新たな知見が得られて楽しかったです😊
オフラインだとエンジニアの知識が豊富な人が多そうという偏見があって、参加しづらいですが
オンラインだと気軽に参加できて学んだことを簡単につぶやけていいですね
途中、疲れて離脱しましたが、LT会が行われたり、PWAのあるあるをTwitterで募集していたりと
イベント盛りだくさんという感じでした。
毎月、第3水曜日にイベントが行われているそうなので、時間が合えば参加してみたいですね😆

## 参考

[PWA Night Conference 2021](https://conf2021.pwanight.jp/)

その他、紹介されていたもの
[web.dev(Web全般を学ぶなら)](https://web.dev/)
[onesignal](https://onesignal.com/)
[FuguAPI](https://github.com/GoogleChromeLabs/fugu-tracker)
