---
title: "AWS初学者がVPCについて学んだことを紹介する"
emoji: "🔰"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, vpc, インフラ, 初心者]
published: true
---

## [データセンター](https://aws.amazon.com/jp/compliance/data-center/)

データセンターとは、サーバやデータセンターなどの IT 機器をまとめて置いておく場所のことです。

## アベイラリティゾーン(AZ)

1 つ以上のデータセンターの集まりであり、
各 AZ は互いに 100km(60 マイル)離れています。
参考として東京リージョンでは 1a,1c,1d の 3 つの AZ があります。(古いアカウントだと 1b も使えるようです)

## [リージョン](https://aws.amazon.com/jp/about-aws/global-infrastructure/regions_az/)

AZ の集まりです。
通信速度などを考えると、サービス提供場所にできるだけ近いリージョンを選ぶとよいでしょう。
日本では、初のリージョンが 2011 年に東京リージョンとして誕生しました。
そして、2 つめのリージョンがちょうど 10 年目の 2021/03/02 に[大阪で誕生](https://aws.amazon.com/jp/local/osaka-region/)しました 🎉

作られたばかりということもあり、東京リージョンにはあって大阪リージョンにはないサービスもあるので、
勉強のためなど特にリージョンにこだわりがないのであれば東京リージョンを選んでおくとよいかもしれません。

## [VPC(Amazon Virtual Private Cloud)](https://aws.amazon.com/jp/vpc/)

AWS で用意された仮想ネットワークを構築するためのサービス。
VPC はネットワーク環境を簡単に構築でき、IP アドレスの範囲の選択やサブネットの作成などを設定できます。
どの通信を許可するかなどファイアウォールの設定(**セキュリティグループ**とよぶ)も可能です。

AWS にログインしたときに 1 つだけデフォルトで作成された VPC(デフォルト VPC)がありますが、
デフォルト VPC は基本的に利用せずに、個別に作成します。
VPC を構築したあとは VPC 内に EC2 など配置するので、理解必須なサービスです。

## [サブネット](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Subnets.html)

VPC で作成されたネットワークを小さく分割したネットワークです。
サブネットは AZ をまたがって、作成することができません。
VPC とサブネットは作成するときに、それぞれ IP アドレスの範囲を設定します。
:::message alert
VPC の IP アドレスのネットワーク部は/16〜/28 の範囲内で作成しなければいけません。
:::
サブネットには、パブリックサブネットとプライベートサブネットの 2 種類あります。
:::details パブリックサブネットとプライベートサブネットについて

- パブリックサブネットは、ネットワーク接続**可能**(インターネットゲートウェイへのルーティングあり)です。
  AWS では、デフォルトゲートウェイにインターネットゲートウェイの設定がされているサブネットのことです。

- プライベートサブネットは、ネットワーク接続**不可**(インターネットゲートウェイへのルーティングなし)です。
  AWS では、デフォルトゲートウェイにインターネットゲートウェイの設定がされていないサブネットのことです。
  :::
  一般に、障害が起こったときのためにサブネットを同じ構成にして複数の AZ を冗長的に配置します。

## ルートテーブル(Route Table)

サブネットに関連づけて使用され、サブネットから外に出る通信をどこに向けて発信するのかを決めるルールの集まりです。
デフォルトでは下記のようなルールが作成されており、削除することはできません。
|送信先|ターゲット|
| --- | --- |
|10.0.0.0/21|local|
ターゲットの「local」は VPC 内部を表し、VPC 内のすべてのリソースの通信を許可します。
ルールの優先順は IP アドレスの範囲が狭いところから適用されます。

## [インターネットゲートウェイ(Internet GateWay)](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Internet_Gateway.html)

VPC にアタッチすることで VPC 内のリソースをインターネットに接続することが可能になるサービスです。
アクセスが増えて負荷が大きくなっても、自動でスケールするため可用性が高いです。
下記テーブルのように、サブネットのルートテーブルを設定して使用します。

| 送信先      | ターゲット       |
| ----------- | ---------------- |
| 10.0.0.0/21 | local            |
| 0.0.0.0/0   | Internet GateWay |

デフォルトで飛ぶ先が指定された先を**デフォルトゲートウェイ**と呼びます。

## [NAT ゲートウェイ(Nat GateWay)](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-nat-gateway.html)

プライベートサブネットがネットワークに接続するために使用されます。
アウトバウンド(中から外への発信)はできますが、インバウンド(外から中への受信)はできません。
インターネットゲートウェイと同様に負荷が大きくなると、自動でスケールしてくれます。
下記テーブルのように、サブネットのルートテーブルを設定して使用します。

| 送信先      | ターゲット  |
| ----------- | ----------- |
| 10.0.0.0/21 | local       |
| 0.0.0.0/0   | Nat GateWay |

## [ENI(Elastic Network Interface)](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/using-eni.html)

NAT ゲートウェイなど VPC 内のインスタンスにアタッチして使用します。
IP アドレスを付与してくれており、EC2 にはデフォルトで 1 つアタッチされています。
1 つのインスタンスに複数の ENI をアタッチすることも可能です。

## IP アドレス

- パブリック IP アドレス

  自動割当が有効になっていれば、EC2 インスタンス作成時に自動で付与されます。
  インターネットと通信するときに必要です。
  インスタンスが再起動、停止、終了したときに解放されます。

- [Elastic IP アドレス](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

  パブリック IP アドレスと同様にインターネットと通信するときに必要です。
  静的な IP アドレスです。
  インスタンスが再起動、停止、終了しても解放されず、同じ IP アドレスが使用可能です。

:::message alert
アタッチしていないと料金がかかるため、不要な Elastic IP アドレスは
解放しましょう。
:::

:::message
VPC 内では、プライベート IP アドレスで通信を行います。
インターネットではパブリック IP アドレスで通信を行います。
:::

## セキュリティグループ(SecurityGroup)

AWS の仮想ファイアウォールサービスです。
IP アドレスの範囲やセキュリティグループ単位などで通信が許可するかを設定します。
IP アドレスで設定する場合は範囲が広いほうを優先して許可されます。
サブネット単位ではなく、EC2 や ENI などのコンポーネント単位で設定を行います。
(サブネット単位で指定したい場合は後述のネットワーク ACL を使います)
アウトバウンドのルールで許可されていれば、インバウンドのルールで拒否されません。
(**ステートフルインスペクション**と呼ばれる機能で動的に通信の許可を判断します)

## [ネットワーク ACL(NetWork Access Control List)](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-network-acls.html)

サブネット単位で設定するファイアウォールです。
ルール番号が付与され、ルール番号が小さい方から評価し、マッチすれば
それ以降のルールは無視されます。
デフォルトですべての通信を拒否するルールが設定されており、
どのルールにもマッチしなければすべての通信が拒否されます。
まずセキュリティグループで対策を行い、それでも対応できなければネットワーク ACL を使います。

## 参考 URL

[データセンター](https://kronoz.co.jp/column/03/)
[データセンター(AWS)](https://aws.amazon.com/jp/compliance/data-center/)
[リージョン](https://aws.amazon.com/jp/about-aws/global-infrastructure/regions_az/)
[大阪リージョン誕生](https://aws.amazon.com/jp/local/osaka-region/)
[リージョンごとの利用可能サービス](https://aws.amazon.com/jp/about-aws/global-infrastructure/regional-product-services/)
[サブネット](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Subnets.html)
[ルートテーブル](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Route_Tables.html)
[インターネットゲートウェイ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Internet_Gateway.html)
[NAT ゲートウェイ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-nat-gateway.html)
[ENI](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/using-eni.html)
[ElasticIP アドレス](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

## 謝辞

この記事は AWS 初学者を導く体系的な動画学習サービス
「CloudTech」の課題カリキュラムで作成しました。
https://kws-cloud-tech.com
