---
title: "Dockerでコンテナの作成からイメージの削除までしてみた"
emoji: "🐳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [docker, cli, コンテナ, イメージ]
published: true
---

Apache を題材にしてコンテナの作成、起動、停止、確認、削除をしてみました。
最後にdockerイメージの削除もしました。
動作確認するにはDocker Engineを起動しておく必要があります。

## 起動しているコンテナの確認

ps コマンドで起動しているコンテナの一覧を表示できます。
オプションとして"a"をつけるとすべてのコンテナを確認できます。

```bash
docker ps -a

# 実行結果(コンテナが作成されてなければ下記のようになる)
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## コンテナの作成、コンテナの起動

run コマンドで Apache のイメージ(httpd)から「apa000ex1」という名前のコンテナを作成・起動します。
初回はイメージをダウンロードするため時間🕑がかかります。
pオプションでホストのポート番号(下記の例では8080)とコンテナのポート番号(下記の例では80)をつなげます。
ホストのポート番号は他とかぶらなければ任意の数字でOKです👍

```bash
docker run --name apa000ex1 -p 8080:80 -d httpd
```

実行できたらコンテナを確認してみましょう。(コンテナ ID はランダムな文字列です。)
STATUS が Up だと起動しています。

```bash
docker ps -a

# 実行結果
CONTAINER ID   IMAGE     COMMAND              CREATED         STATUS         PORTS                  NAMES
7f142d6453dc   httpd     "httpd-foreground"   6 seconds ago   Up 4 seconds   0.0.0.0:8080->80/tcp   apa000ex1
```

ポートの設定をしたので"http://localhost:8080/"に接続すると画像のような画面が表示されます。
!["http://localhost:8080/"の画面](https://gyazo.com/765a1d6b729e8776bd3b1af32b03413f.png =300x)

## コンテナの停止

stop または kill コマンドでコンテナを停止できます。
kill コマンドは強制停止させます。

```bash
docker stop apa000ex1
```

実際に停止しているかどうかはpsコマンドで確認可能です。
STATUSが"Exited"だと停止しています。

```bash
docker ps -a
# 実行結果 STATUSが"Exited"であることから停止していることがわかる
CONTAINER ID   IMAGE     COMMAND              CREATED       STATUS                   PORTS     NAMES
7f142d6453dc   httpd     "httpd-foreground"   2 hours ago   Exited (0) 2 hours ago             apa000ex1
```

もちろん、"http://localhost:8080/"に接続してもアクセスできません。

![コンテナ停止後の"http://localhost:8080/"の画面](https://gyazo.com/86a4d5a8c85b2dda785eedeaacb0b4e2.png =300x)

## コンテナの再起動

停止したコンテナを再び実行するには start コマンドを使います。startコマンドではポート番号の指定は不要です。

```bash
docker start container apa000ex1
```

## コンテナの削除

rm コマンドでコンテナの削除ができます。削除する前にはstopコマンドでコンテナの停止を事前にしておく必要があります。

```bash
docker rm apa000ex1
```

削除されているか確認してみます。

```bash
docker ps -a
# 実行結果
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

コンテナが表示されていないことから削除されていることを確認できました。

:::message
コンテナの停止やコンテナの再起動を行うときに、名前ではなくコンテナ ID を指定しても OK です。
コンテナ ID は docker ps (-a) コマンドで確認しましょう。

```bash
docker stop 7f142d6453dc
```

:::

## イメージの削除

コンテナを削除してもイメージは残り続けます。
イメージが残るとストレージを圧迫するので、不要なイメージは"docker rmi"で削除してしまいましょう。

### イメージの確認
コンテナを削除してもイメージが残っているか確認します。
```bash
docker images

# 実行結果
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
httpd        latest    479801e882f4   4 days ago   131MB
```

### イメージの削除
rmiコマンドでイメージを削除できます。
コンテナのときと同様イメージIDを指定して、削除できます。
イメージIDで削除する場合は、docker imagesで確認したイメージIDを指定します。
```bash
docker rmi httpd

# こちらでも削除できる
docker rmi 479801e882f4
```

### イメージが削除されているか確認
何も表示されていなければ削除できています。
```bash
docker images

# 実行結果
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

## 参考

[kill コマンドについて](https://docs.docker.com/engine/reference/commandline/kill/)
[仕組みと使い方がわかる Docker＆Kubernetes のきほんのきほん](https://book.mynavi.jp/ec/products/detail/id=120304)
