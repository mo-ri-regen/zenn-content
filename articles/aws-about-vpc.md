---
title: "AWS初学者がVPCについて学んだことを紹介する"
emoji: "🔰"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, vpc, インフラ, 初心者]
published: true
---

## [データセンター](https://aws.amazon.com/jp/compliance/data-center/)

データセンターとは、サーバやデータセンターなどのIT機器をまとめて置いておく場所のこと。


## アベイラリティゾーン(AZ)

1つ以上のデータセンターの集まり。
各AZは互いに100km(60マイル)離れている。
参考として東京リージョンでは1a,1c,1dの3つのAZがある。(古いアカウントだと1bも使えるらしい)

## [リージョン](https://aws.amazon.com/jp/about-aws/global-infrastructure/regions_az/)

AZの集まり。通信速度などを考えて、サービス提供場所に
できるだけ近いリージョンを選ぶとよい。
日本では、初のリージョンが2011年に東京リージョンが誕生して以来、2つめのリージョンがちょうど10年目の2021/03/02に[大阪リージョンが誕生](https://aws.amazon.com/jp/local/osaka-region/)した🎉

できたばかりで、東京リージョンにはあって大阪リージョンにはないサービスもたまにあるので、
勉強のためなどで特にリージョンにこだわりがないのであれば東京リージョンを選んでおくといいかも。

## [VPC(Amazon Virtual Private Cloud)](https://aws.amazon.com/jp/vpc/)

AWSで用意された仮想ネットワークを構築するためのサービス。<!--どのリージョンに作成するかを最初に設定する。-->
VPCはネットワーク環境を簡単に構築でき、IPアドレスの範囲の選択やサブネットの作成などを設定できる。どの通信を許可するかなどファイアウォールの設定(**セキュリティグループ**とよぶ)も可能。

AWSにログインしたときに1つだけデフォルトで作成されたVPC(デフォルトVPC)があるが、
デフォルトVPCは基本的に利用せずに、個別に作成する。
VPCを構築したあとは、VPC内にEC2など配置するので、理解必須なサービス。

## [サブネット](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Subnets.html)

VPCで作成されたネットワークを小さく分割したネットワーク。
サブネットはAZをまたがって、作成することができない。
VPCとサブネットは作成するときに、それぞれIPアドレスの範囲を設定する。
:::message alert
VPCのIPアドレスのネットワーク部は/16〜/28の範囲内で作成しなければならない。
:::
サブネットには、パブリックサブネットとプライベートサブネットの2種類ある。
:::details パブリックサブネットとプライベートサブネットについて

- パブリックサブネットは、ネットワーク接続**可能**(インターネットゲートウェイへのルーティングあり)
AWSでは、デフォルトゲートウェイにインターネットゲートウェイの設定がされているサブネットのことである。

- プライベートサブネットは、ネットワーク接続**不可**(インターネットゲートウェイへのルーティングなし)
AWSでは、デフォルトゲートウェイにインターネットゲートウェイの設定がされていないサブネットのことである。
:::
一般に、障害が起こったときのためにサブネットを同じ構成にして複数のAZを冗長的に配置する。


## ルートテーブル(Route Table)

サブネットに関連づけて使用され、サブネットから外に出る通信をどこに向けて発信するのかを決めるルールの集まり。
デフォルトでは下記のようなルールが作成されており、削除することはできない。
|送信先|ターゲット|
| --- | --- |
|10.0.0.0/21|local|
ターゲットの「local」はVPC内部を表し、VPC内のすべてのリソースの通信を許可する。
ルールの優先順はIPアドレスの範囲が狭いところから適用される。

## [インターネットゲートウェイ(Internet GateWay)](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Internet_Gateway.html)

VPCにアタッチすることでVPC内のリソースをインターネットに接続することが可能になるサービス。
アクセスが増えて負荷が大きくなっても、自動でスケールするため可用性が高い。
下記テーブルのように、サブネットのルートテーブルを設定して、使用する。

|送信先|ターゲット|
| --- | --- |
|10.0.0.0/21|local|
|0.0.0.0/0|Internet GateWay|

デフォルトで飛ぶ先が指定された先を**デフォルトゲートウェイ**と呼ぶ。

## [NATゲートウェイ(Nat GateWay)](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-nat-gateway.html)

プライベートサブネットがネットワークに接続するために使用される。
アウトバウンド(中から外への発信)はできるが、インバウンド(外から中への受信)はできない。
インターネットゲートウェイと同様に負荷が大きくなると、自動でスケールしてくれる。
下記テーブルのように、サブネットのルートテーブルを設定して、使用する。

|送信先|ターゲット|
| --- | --- |
|10.0.0.0/21|local|
|0.0.0.0/0|Nat GateWay|

## [ENI(Elastic Network Interface)](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/using-eni.html)

NATゲートウェイなどVPC内のインスタンスにアタッチして使用する。
IPアドレスを付与してくれており、EC2にはデフォルトで1つアタッチされている。
1つのインスタンスに複数のENIをアタッチすることも可能。

## IPアドレス

- パブリックIPアドレス

自動割当が有効になっていれば、EC2インスタンス作成時に自動で付与される。
インターネットと通信するときに必要。
インスタンスが再起動、停止、終了したときに解放される。


- [Elastic IPアドレス](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

パブリックIPアドレスと同様にインターネットと通信するときに必要。
静的なIPアドレス。
インスタンスが再起動、停止、終了しても解放されず、同じIPアドレスが使用可能。

:::message alert
アタッチしていないと料金がかかるため、不要なElastic IPアドレスは
解放しよう。
:::

:::message
VPC内では、プライベートIPアドレスで通信を行う。
インターネットではパブリックIPアドレスで通信を行う。
:::

## セキュリティグループ(SecurityGroup)

AWSの仮想ファイアウォールサービス。
IPアドレスの範囲やセキュリティグループ単位などで通信が許可するかを設定する。
IPアドレスで設定する場合は範囲が広いほうを優先して許可される。
サブネット単位ではなく、EC2やENIなどのコンポーネント単位で設定を行う。
(サブネット単位で指定したい場合は後述のネットワークACLを使う)
アウトバウンドのルールで許可されていれば、インバウンドのルールで拒否されない。
(**ステートフルインスペクション**と呼ばれる機能で動的に通信の許可を判断する)

## [ネットワークACL(NetWork Access Control List)](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-network-acls.html)

サブネット単位で設定するファイアウォール。
ルール番号が付与され、ルール番号が小さい方から評価し、マッチすれば
それ以降のルールは無視される。
デフォルトですべての通信を拒否するルールが設定されており、
どのルールにもマッチしなければすべての通信が拒否される。
まず、セキュリティグループで対策を行い、それでも対応できなければネットワークACLを使う。

## 参考URL

[データセンター](https://kronoz.co.jp/column/03/)
[データセンター(AWS)](https://aws.amazon.com/jp/compliance/data-center/)
[リージョン](https://aws.amazon.com/jp/about-aws/global-infrastructure/regions_az/)
[大阪リージョン誕生](https://aws.amazon.com/jp/local/osaka-region/)
[リージョンごとの利用可能サービス](https://aws.amazon.com/jp/about-aws/global-infrastructure/regional-product-services/)
[サブネット](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Subnets.html)
[ルートテーブル](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Route_Tables.html)
[インターネットゲートウェイ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Internet_Gateway.html)
[NATゲートウェイ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-nat-gateway.html)
[ENI](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/using-eni.html)
[ElasticIPアドレス](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

## 謝辞

この記事はAWS初学者を導く体系的な動画学習サービス
「AWS CloudTech」の課題カリキュラムで作成しました。
https://aws-cloud-tech.com