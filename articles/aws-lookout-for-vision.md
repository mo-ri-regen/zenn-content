---
title: "AWS関西女子会主催 LookoutforVisionのハンズオンを体験してみた"
emoji: "✍️"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [AWS, LookoutForVision, jawsug, jawsugkgirls, AWSUserGroups]
published: true
---

## 概要

[前回のハンズオンイベント](https://zenn.dev/mo_ri_regen/articles/jawsdays2021-handson)に引き続き、JAWS-UG🦈 主催の[AWS のハンズオンイベント](https://jawsugkgirls.doorkeeper.jp/events/119358)に参加してきました。
男子も参加 OK と書いてましたが、「関西"女子会"」というコミュニティなので
女子だらけ 👩‍💻 で馴染めなかったら、どうしようとビクビクしながら参加しました。
当日は 20 名程度参加しており、(メンターが男性だったからかもしれませんが)
女子会という感じではなく、終始和やかな雰囲気でした 😊
コロナで、大変な目に合った人もいるかたもおられると思いますが、
逆に、オンラインイベントを主流にしてくれた部分もあるのでよかったなと思います。
もしこのイベントがオフライン開催だと女子だらけだったときを考えると、多分、参加しなかっただろうなと思います。

## 内容

[Lookout for Vision](https://aws.amazon.com/jp/lookout-for-vision/)をハンズオン形式で学ぶというものでした。
Lookout for Vision とは転移学習と呼ばれるものを使って、ある製品を正常品か不良品か判別することができるサービスです。
内容としては機械学習の分野ですが、使う分には特に統計や数学の知識が必要ではないので、気軽に試すことができます。もともと、AWS には[sagemaker](https://aws.amazon.com/jp/sagemaker/)(こちらも転移学習をつかっているそうです)を使って、同様のことはできるそうですが、sagemaker は
数学の知識が必要らしいので、Lookout for Vision のほうが気軽に使うことができます。
他にも[sagemaker jump star](https://docs.aws.amazon.com/sagemaker/latest/dg/studio-jumpstart.html)というサービスもあり AWS って奥が深いなと思いました。

## ハンズオンの様子

ハンズオン中は使っているサービスの特性上、待ち時間(学習時間)が長く、
その間、参加者の自己紹介や機械学習の話をしていました。

参加者の中には[AWS の認定資格(多分、MachineLearning)](https://aws.amazon.com/jp/certification/?nc2=sb_ce_co)取得を目指しているかたや業務で機械学習をされているかたなどさまざまな方が参加していました。

個人的に興味深かった話は、「正常品を異常品と判定する」ことと、「異常品を正常品と判定する」ことはロジックでは同じらしいですが、ビジネス的には意味が異なる(食べ物などは異常品を正常と判定してしまうと、その時点でアウト)ので混合行列を使って、
TP(TruePositive),TN(TrueNegative)
FP(FalsePositive),FN(FalseNegative)
で表すという話です。
~~学生のとき座学で聞いたような気がしますが、忘れました。~~

## 最終結果

ハンズオンで作成したモデルの結果は下記の通りになりました。
![最終結果](https://gyazo.com/d94559c6e797ce9a87367a7262e8ae50.png)
学習データが正常品 20 枚、異常品が 10 枚と数が少なかったからというのもあると思いますが、普通は 100%がこんなに続きません。
実際の現場では、このモデルを使って、未知のデータに対して正常か異常か判定します 👮‍♀️

## 感想

AWS っていろいろできるなと改めて思いました。
多分、1 人だとマニアックなサービスをあえて触ろうと思わないですが、
こうしてハンズオン形式でイベントをやってくださるといろんなサービスに触れることができて楽しかったです。

ハンズオンだけでなく、いろいろお話が聞けました。
たとえば、女子だと周りが男性が多くて、苦労するって話を聞けたり、データサイエンティストと営業だけだと話が噛み合わないから間に翻訳する人必要だよねって話を聞けたりして面白かったです。

社内では Azure 使っているので、Azure でも似たようなサービスがないか興味を持ちました。
実務で使えるかというと微妙かもしれないですが、視野を広げることができるので定期的に
JAWS のイベントは参加したいなと思いました。(さっそく 4/27(火)に[イベント](https://jawsug-bgnr.connpass.com/event/210736/)あるみたいです。)

## URL

[使用したサービス:Lookout for Vision](https://aws.amazon.com/jp/lookout-for-vision/)
[今回のイベント](https://jawsugkgirls.doorkeeper.jp/events/119358)
[JAWS-UG](https://jaws-ug.jp/for-participant/)
