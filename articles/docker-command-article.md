---
title: "Dockerのコマンドについて"
emoji: "🐳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [docker]
published: true
---

docker のコマンドを使うことでコンテナの起動やイメージの作成などを行うことができます。

## 基本形

```bash
docker コマンド (オプション) 対象 (引数)
```

コマンドは上位コマンドと副コマンドで構成されています。上位コマンドでは「何を」という部分を指定し、副コマンドでは「どうする」という部分を指定します。コマンドによっては上位コマンドを省略して副コマンドのみで記述できます。
対象では、コンテナ名など具体的な名前が入ります。オプションと引数は、ない場合もあります。

- 例

```bash
docker container run -d hoge --model=1
```

container という上位コマンドと run という副コマンドで構成されています。

## 上位コマンド

上位コマンドは 12 種類あります。[参考本](https://book.mynavi.jp/ec/products/detail/id=120304)によると太字をまずは理解しようとのことです。

| 上位コマンド  | 内容                                                                      |
| ------------- | ------------------------------------------------------------------------- |
| **container** | コンテナの操作を行う                                                      |
| **image**     | イメージに関する操作を行う                                                |
| **volume**    | ボリューム(コンテナからマウントできるストレージ)の操作を行う              |
| **network**   | Docker ネットワークに関する操作を行う                                     |
| checkpoint    | 現在の状態を一時的に保存し、後でその時点に戻ることができる                |
| node          | Docker Swarm のノードを管理する機能                                       |
| plugin        | プラグインを管理する機能                                                  |
| secret        | Docker swarm のシークレット機能を管理する機能                             |
| service       | Docker swarm のサービスを管理する機能                                     |
| stack         | Docker swarm や Kubernetes でサービスをひとまとめにしたスタックを管理する |
| swarm         | Docker swarm を管理する                                                   |
| system        | Docker Engine の情報を取得する                                            |

## 単独コマンド

上位コマンドをもたないコマンドです。

| コマンド | 内容                                     |
| -------- | ---------------------------------------- |
| login    | Docker レジストリにログインする          |
| logout   | Docker レジストリからログアウトする      |
| search   | Docker レジストリで検索する              |
| version  | Docker Engine およびバージョンを表示する |

## 参考

[仕組みと使い方がわかる Docker＆Kubernetes のきほんのきほん](https://book.mynavi.jp/ec/products/detail/id=120304)
