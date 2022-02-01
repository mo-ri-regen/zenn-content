---
title: "yarnコマンドが使えないと思ったら"
emoji: "🤔"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [yarn, error, エラー, ポエム]
published: true
---

## 結論

エラー原因を調べて見たら、プロジェクトとは関係のないディレクトリで yarn コマンドを使っていました

## エラー内容

```bash
yarn dev
```

と入力すると下記のようなエラーが出ました。

```bash
yarn run v1.22.11
error Couldn't find a package.json file in "/foo/bar/baz"
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```

package.json が見つからないと書かれているので VSCode で確認すると、
![package.jsonはインストールされている](https://gyazo.com/0192367c5d0f88309123c85e00d01686.png=50x)

package.json がインストールされていました。

バージョンの問題?と思い、最新版の npm と yarn をインストールしたり
他にもいろいろコマンドを叩いたりすると、違うエラーが出て解決しませんでした。

```bash
yarn run v1.22.17
warning package.json: No license field
error Command "dev" not found.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```

ここで、思いつきでディレクトリを確認してみました。
案の定、package.json がインストールされていたディレクトリとエラーが出ていたディレクトリが違っていました。

どのディレクトリに対して実行しているかきちんと確認しようと思いました。
