---
title: "docker-composeコマンドで複数のコンテナを起動する"
emoji: "👩‍💻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [docker, dockercompose]
published: true
---

Docker-compose を使うと簡単に複数のコンテナを起動できます。
コンテナを起動するためには docker-compose.yml を作成しておく必要があります。

docker-compose では-f オプションコマンドを使うと複数の compose ファイルの指定や docker-compose.yml 以外のファイル名の実行ができます。

## ビルド

```bash:shell
docker-compose build
```

Dockerfile やビルドするディレクトリを変更したときはビルドしましょう

### オプション

- --no-cache
  キャッシュを使わずにビルドをします
- -- force-rm
  すぐにコンテナを削除します

## 作成・起動

```bash:shell
docker-compose up
```

コンテナのビルドから開始

### オプション

- -d
  バックグランドで実行します

- --build
  コンテナを起動する前にビルドをします
- -- remove-orphans
  定義ファイルに定義されていないサービス用コンテナを削除します
  orphan は日本語で「孤児」という意味です。

## 停止・削除

```bash:shell
docker-compose down
```

コンテナを止めて削除します。
イメージを削除するときはオプションで指定します。

### オプション

- --rmi \<type>

  \<type>には"all"か"local"が入ります。
  "all"を指定するとすべてのイメージを削除します。
  "local"を指定するとイメージフィールドにカスタムタグがセットされていないイメージが削除されます。

- -v
  docker-compose.yml の"volumes"で定義したボリュームを削除します。

## 参考

[公式ドキュメント](https://docs.docker.com/compose/reference/)
[仕組みと使い方がわかる Docker＆Kubernetes のきほんのきほん](https://www.amazon.co.jp/dp/B08T961HKP/)
