---
title: "デプロイをするときにCDKでよく使うコマンド一覧"
emoji: "💻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, cdk]
published: true
---

## はじめに

AWS をソースコードで管理するのに CDK があると知ったためまとめました。

学習では公式チュートリアルを実際に動かしてみるのをオススメします。
https://catalog.workshops.aws/typescript-and-cdk-for-beginner/ja-JP/40-cdk-introduction/10-create-project/10-cdk-init

CDK を使うとコマンドを叩くだけで AWS のリソースをすぐ作れるため
同じリソースをミスなくすぐに作れます。

## コマンド

- テンプレートファイル作成

init コマンドを使うとテンプレートコマンドが作成されます。

```bash
cdk init sample-app --language=typescript
```

:::message
sample-app のところは下記 3 パターンのオプションがあります。
app (デフォルト)：新しい CDK アプリケーションを作成
sample-app：サンプルコード付きの CDK アプリケーションを作成
lib：CDK コンストラクトライブラリの開発用プロジェクトを作成
:::

実行すると下記ファイルが生成されます。

```bash
tree -I "node_modules/"

cdk_workshop/
|-- bin
|   |-- cdk_workshop.ts
|-- lib
|   |-- cdk_workshop-stack.ts
|-- test
|   |-- cdk_workshop.test.ts
|-- node_modules/
|-- README.md
|-- cdk.json
|-- jest.config.js
|-- package-lock.json
|-- package.json
|-- tsconfig.json
|-- .npmignore
|-- .gitignore
```

:::message
bin/cdk_workshop.ts
lib/cdk_workshop-stack.ts
test/cdk_workshop.test.ts
の cdk_workshop の部分はディレクトリと同じ名前になります。
:::

- CloudFormation のテンプレート確認

CDK では ソースコードから CloudFormation が作成されます。synth コマンドでどのような CloudFormation のテンプレートが出力されるか確認できます。

```bash
cdk synth
```

- 初めてデプロイするとき

デプロイをする前に実行します。

```bash
cdk bootstrap
```

:::message
一度、実行したら二回目以降は実行不要です。
:::

- 差分確認

```bash
cdk diff
```

- デプロイ

```bash
cdk deploy
```

:::message
リソースを作成されるため料金が発生する可能性があります
deploy をするときは diff コマンドで内容を確認してから実行しましょう。
:::

https://docs.aws.amazon.com/ja_jp/cdk/v2/guide/ref-cli-cmd-deploy.html

- リソースの削除

リソースの作りっぱなしは料金が発生するので
今後、使用する予定がない場合は必ず削除コマンドを実行しましょう！

```bash
cdk destroy
```

## 参考

- チュートリアル

https://catalog.workshops.aws/typescript-and-cdk-for-beginner/ja-JP

- ドキュメント

https://docs.aws.amazon.com/cdk/api/v2/docs/aws-construct-library.html

- 実際のチュートリアルの様子

https://zenn.dev/mo_ri_regen/scraps/59400f57fb72e0
