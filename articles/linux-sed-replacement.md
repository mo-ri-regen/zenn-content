---
title: "sedによる文字列の置換方法"
emoji: "🌘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [cli, linux, linuxコマンド]
published: true
---

sed(Stream EDiter)を使うとテキストの編集が行えます。
sed を使って文字列の置換[^1]することができます。。

[^1]: 今回は説明しませんが d オプションを指定すると削除することができます。

## 使い方

```bash:bash
sed -i s/検索パターン/置換パターン ファイル名
```

sed はオプションを指定しないとファイルの上書き保存は行わないため i オプションで上書きする必要があります。"s"を指定すると置換できます。

:::message
i オプションを指定せずに置換した結果を保存したい場合はリダイレクト記号">"を使って別ファイルに保存する必要があります。
:::

### 例

```txt:example.txt
redhat linux linux2
centos linux
```

example.txt の"linux"を"LINUX"に置換するには下記のコマンドを実行します。

```bash:bash
sed -i s/linux/LINUX example.txt
```

置換した結果は下記の通りとなります。

```txt:example.txt
redhat LINUX linux2
centos LINUX
```

example.txt の 1 行目の linux2 も置換するには後述の g スイッチを記述します。

## 全置換

s コマンドだけを指定すると指定した文字列が 1 行に複数箇所あった場合は最初にマッチした文字列だけ置換するため、すべてを置換するには最後に g スイッチを指定する必要があります。

```bash:bash
sed -i s/検索パターン/置換パターン/g ファイル名
```

### 例

```txt:example.txt
redhat linux linux2
centos linux
```

先程と同様、example.txt の"linux"という文字列を"LINUX"に置換します。

```bash:bash
sed -i s/linux/LINUX/g example.txt
```

実行結果は下記の通りになります。

```txt:example.txt
redhat LINUX LINUX2
centos LINUX
```
