---
title: "AWSのCLIを設定してみる"
emoji: "👩‍🏫"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, CLI]
published: true
---

## この記事の目的

aws configure を使ってCLIの設定方法を学ぶ📚

## はじめに

AWSではコンソール画面からクリックすることでいろいろ設定ができます。
しかし、画面が定期的にアップデートされるため参考にしていた画面が今の画面と異なることがよくあります。

AWSのCLIを使えばAWSの画面のアップデートに左右されずに、ターミナル上で設定を行うことができます。

## 実行環境

Macbook Air(M1)
ターミナル:fish ver 3.2.2

:::message
WindowsでもCLIはインストールできますが、動作確認はしていません
:::

## 準備

AWSでIAMユーザを作成してください。(過去にIAMユーザを作成した[記事]([過去](https://zenn.dev/mo_ri_regen/articles/aws-iam-with-administrator-rights))もあるのでよければ参考にしてください。)

## インストール

CLIは[こちら](https://aws.amazon.com/jp/cli/)からダウンロードできます。

下記コマンドを入力してインストールされているか確認しましょう👀

```bash
aws --version
```

## 設定

下記コマンドを入力すると対話的に設定ができます。

```bash
aws configure
```

![aws configureで設定](https://gyazo.com/310680a4708a9f58fa7205fa99877e44.png)

- Access Key
IAMの左ペイン アクセス管理→ユーザをクリック。確認したいユーザを選択→認証情報
のところでAccessKeyを確認できます。(ない場合は作成してください)
(文章だけだとわかりづらいかもしれないので、~~気が向いたら~~記事にします✍️)

- Secret Access Key
キーを作成するときにのみSecret Access Keyを確認できます。
わからない場合はAccessKeyをもう一度作成してください。

- Default region name
デフォルトでリクエストを送信するサーバのAWSリージョンを設定します。東京(ap-north-east-1)に設定しました。

- Default output format
出力結果の形式を選択します。デフォルトは"json"です。
json,yaml,yaml-stream,text,tableの中から選びます。(yamlはCLIのバージョン2で使用可能)

間違えて入力した場合でも、もう一度"aws configure"と打てば再設定できます。

:::details リージョン名("ap-north-east-1"の部分)の確認方法

[公式ページ](https://docs.aws.amazon.com/general/latest/gr/rande.html)でも確認できますが、簡単な方法としてコンソール画面の右上の地域のところを確認すれば一覧が出てきます。
![リージョン名確認](https://gyazo.com/df3cbd105d227923d9d666c73d9230e0.png)

東京の場合は"ap-northeast-1"となっていますね😊
:::

## プロファイル

設定のコレクションをプロファイルと呼びます。
下記コマンドを入力することでプロファイルに名前をつけることができます。

```bash
# 設定例
aws configure --profile produser

# あとは最初にconfigureと打ったときと同様に設定する
AWS Access Key ID [None]: AKIAI44QH8DHBEXAMPLE
AWS Secret Access Key [None]: je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
Default region name [None]: us-east-1
Default output format [None]: text
```

```bash
# プロファイル使用方法
aws s3 ls --profile produser
```

## 参考

https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-configure-quickstart.html

https://aws.amazon.com/jp/cli/
