---
title: "IAMユーザ、IAMグループ、IAMポリシー、IAMロールについて"
emoji: "👸"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, IAM]
published: true
---

今回は[AWSの薄い本　IAMのマニアックな話](https://www.amazon.co.jp/AWS%E3%81%AE%E8%96%84%E3%81%84%E6%9C%AC-IAM%E3%81%AE%E3%83%9E%E3%83%8B%E3%82%A2%E3%83%83%E3%82%AF%E3%81%AA%E8%A9%B1-%E4%BD%90%E3%80%85%E6%9C%A8%E6%8B%93%E9%83%8E-ebook/dp/B085PZCMG2)を読んで学んだIAMの一部分を説明します👨‍🏫

## IAMユーザについて

コンソールにログインするときの認証に使います。
プログラムからログインできるアクセスキーの発行もできるが、
理由がなければしないほうがいいです。
アクセスキーの発行は、管理に注意して最小権限の設定を行います。
IAMユーザは利用者ごとに発行します。
最初のIAMユーザを作成するためだけにrootユーザを使用し、それ以後は
IAMユーザで操作を行います。

## IAMグループ

同じ役割をもつIAMユーザをグループ化する機能です。
IAMユーザに直接、権限を付与すると過剰に権限を与えたり逆に権限が足りない場合があるので、
IAMを運用するときはIAMユーザに直接権限を与えるのではなく、
IAMグループに権限を与えることが推奨されています。

## IAMポリシー

JSON形式で記述をし、どのサービスを許可するかなどの権限の制御をまとめたものです。

誰が、「(Action)どのAWSサービス」の「Resource(どのリソースに対してどんな操作)」を「Effect(許可する or 許可しない)」ということが設定可能です。

```json5

// s3リソースに対してGetとListをそれぞれ許可する
{
  "Version":"2012-10-17", //最新バージョンである"2012-10-17"を指定する
  "Statement":[
    {
      "Effect":"Allow",   //許可(拒否する場合はDeny)
      "Action":[          //許可または拒否するアクションのリスト
        "s3:Get*",
        "s3:List*"
      ]
    }
  ],
  "Resource": "*"
}

```

AWSが最初から設定しているポリシーを**AWS管理ポリシー**とよびます。
各ユーザがそれぞれ設定したポリシーを**カスタマー管理ポリシー**とよびます。
インラインポリシーというのもありますが、古い機能なのでここでは省略します。
ベストプラクティスとして[カスタマー管理ポリシーを使おう](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/best-practices.html#best-practice-managed-vs-inline)ということが書かれてます。
権限の設定方針として足し算でAWS管理ポリシーを設定(必要な権限の許可)して、引き算でカスタマー管理ポリシー(不要な権限の拒否)を設定します。

IAMのベストプラクティスとして[最小権限で設定する](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/best-practices.html#use-groups-for-permissions)と言われているので、
目的に応じた最小権限を設定しましょう。

## IAMロール

AWSサービスやアプリケーションに対してAWSの操作権限を与える仕組みです。

## パーミッション・バウンダリー(Permissions Boundary)

IAMユーザまたはIAMロールに対するアクセス権限として動作し、IAMの移譲権限を制限します。
IAMユーザ(or IAMロール)で付与した権限とboundaryで許可した権限が
重なり合う部分のみ有効となります。
つまり、boundaryで許可していない場合はIAMユーザ(or IAMロール)で
どんなに権限を設定しても一切、使うことができません。

一般的には、組織外の他者に権限を与えるときに使われます。
限定した権限のIAMユーザを貸与したうえで、boundaryを利用すると
意図した以上の権限を渡すことを防ぐことができます。

## 最後に

おそらく最初は権限を与えられる側なのであまり意識する必要はないですが、
IAMによる権限設定は、悪意がある人が行うと大変なことになるので
権限設定できるようになりたいですね😊

## 参考

[AWSの薄い本　IAMのマニアックな話](https://www.amazon.co.jp/AWS%E3%81%AE%E8%96%84%E3%81%84%E6%9C%AC-IAM%E3%81%AE%E3%83%9E%E3%83%8B%E3%82%A2%E3%83%83%E3%82%AF%E3%81%AA%E8%A9%B1-%E4%BD%90%E3%80%85%E6%9C%A8%E6%8B%93%E9%83%8E-ebook/dp/B085PZCMG2)

[IAMについて(公式)](https://docs.aws.amazon.com/ja_jp/iam/index.html)

[IAMのベストプラクティス](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/best-practices.html)

[IAMポリシー](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/access_policies.html)

[IAMポリシー(クラスメソッド)](https://dev.classmethod.jp/articles/aws-iam-policy/)
