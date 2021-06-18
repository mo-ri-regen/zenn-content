---
title: "IAMユーザ、IAMグループ、IAMポリシー、IAMロールについて"
emoji: ""
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, IAM]
published: false
---

今回は[AWSの薄い本　IAMのマニアックな話](https://www.amazon.co.jp/AWS%E3%81%AE%E8%96%84%E3%81%84%E6%9C%AC-IAM%E3%81%AE%E3%83%9E%E3%83%8B%E3%82%A2%E3%83%83%E3%82%AF%E3%81%AA%E8%A9%B1-%E4%BD%90%E3%80%85%E6%9C%A8%E6%8B%93%E9%83%8E-ebook/dp/B085PZCMG2)を読んで学んだIAMの一部分を説明します👨‍🏫

## IAMユーザについて

コンソールにログインするときの認証に使う。
プログラムからログインできるアクセスキーの発行もできるが、
理由がなければしないほうがいい。
アクセスキーの発行は、管理に注意して最小権限の設定を行う。
IAMユーザは利用者ごとに発行する。

## IAMグループ

同じ役割をもつIAMユーザをグループ化する機能。
IAMユーザに直接、権限を付与すると過剰に権限を与えたり逆に権限が足りない場合があるので、
IAMを運用するときはIAMユーザに直接権限を与えるのではなく、IAMグループに権限を与えることが
推奨されている。

## IAMポリシー

JSON形式で記述をし、どのサービスを許可するかなどの権限の制御をまとめたもの

誰が、「(Action)どのAWSサービス」の「Resource(どのリソースに対してどんな操作)」を「Effect(許可する or 許可しない)」ということが設定可能。

```json

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

AWSが最初から設定しているポリシーを**AWS管理ポリシー**とよぶ。
各ユーザがそれぞれ設定したポリシーを**カスタマー管理ポリシー**とよぶ。
権限の設定方針として足し算でAWS管理ポリシーを設定(必要な権限の許可)して、引き算でカスタマー管理ポリシー(不要な権限の拒否)を設定する。

IAMの[ベストプラクティス](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/best-practices.html#grant-least-privilege)として最小権限で設定すると言われているので、
目的に応じた最小権限を設定しましょう。

## IAMロール

## 参考

[IAMポリシー](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/access_policies.html)

[クラスメソッド](https://dev.classmethod.jp/articles/aws-iam-policy/)

[AWSの薄い本　IAMのマニアックな話](https://www.amazon.co.jp/AWS%E3%81%AE%E8%96%84%E3%81%84%E6%9C%AC-IAM%E3%81%AE%E3%83%9E%E3%83%8B%E3%82%A2%E3%83%83%E3%82%AF%E3%81%AA%E8%A9%B1-%E4%BD%90%E3%80%85%E6%9C%A8%E6%8B%93%E9%83%8E-ebook/dp/B085PZCMG2)
