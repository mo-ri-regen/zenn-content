---
title: "MacでPATHを通すときにVimが使えなくなったときの解決策"
emoji: "🔧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [terminal, mac]
published: iterm
---

:::message
メッセージ内容のメモを忘れたため、本来表示されるべきエラーメッセージとは少し異なるかもしれません。
:::

## エラー内容

Vim を使おうとしたら、

```bash
vi: command not found
```

と表示され Vim が使えなくなりました。

## 経緯

[このサイト](https://web-guided.com/1874/)を読むと zsh の設定を変更するには、
.zshrc を編集する必要がありました。
なので、ファイルの中身を確認すると

```txt:.zshrc
export VOLTA_HOME="$HOME/.volta"
export PATH="$VOLTA_HOME/bin:$PATH:/usr/local/opt/php"
```

と記載がありました。
PATH の設定をするために、ファイルを下記のように編集してしまいました。

```txt:.zshrc
export VOLTA_HOME="$HOME/.volta"
export PATH="$VOLTA_HOME/bin:$PATH"
export PATH="/usr/local/opt/php"
```

その後、

```bash
source ~/.zshrc
```

を実行すると

```bash
dirname: command not found
dirname: command not found
```

というエラーが出ました。
zsh の設定を見直そうとすると

```bash
vi: command not found
```

というエラーが出て Vim が使えなくなりました 😱

## 原因

[環境変数の設定を間違えてほとんどのコマンドが command not found になってしまったときの対処法](https://qiita.com/noraworld/items/4556f91bc31f641d187d)を読むと、
原因は export path を複数宣言したため、後者に宣言された PATH で更新されてしまったからのようです。

## 解決策

PATH を編集するときは、コロンで繋げる必要があるようです。

ホームディレクトリの直下(/Users/{ユーザ名}/.zshrc) にあることはわかったため、VScode から下記のように編集しました。

```txt:.zshrc
export VOLTA_HOME="$HOME/.volta"
export PATH="$VOLTA_HOME/bin:$PATH:/usr/local/opt/php"
```

そしてターミナルを再起動したあと

```bash
source .zshrc
```

を実行するとエラーが出ませんでした。
vim も実行できるようになりました 🎉

## 参考

- PATH の設定
  [PHP 7.4 を Homebrew でインストールした時に command not found になる](https://web-guided.com/1874/)
- エラー解決
  [環境変数の設定を間違えてほとんどのコマンドが command not found になってしまったときの対処法](https://qiita.com/noraworld/items/4556f91bc31f641d187d)
