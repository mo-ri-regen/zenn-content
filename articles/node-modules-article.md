---
title: "node_modulesの再インストール方法"
emoji: "🌳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [nodemodules, yarn, npm]
published: true
---

パッケージをインストールしたあと、node_modulesができますが
チームで共有する場合は、ファイルの大きさからnode_modulesを共有することはありません。
なので、node_modulesを再インストールする方法を紹介します。

## 動作確認環境

yarn 1.22.10
(npmは確認してません)

## 対処法について

下記の画像のようにnode_modulesがあります
![node_modulesあり](https://gyazo.com/15f06fe4bd1b7dd8033bde95b5b7ba6a.png)

実際にnode_modulesを削除してみます。
![node_modules削除](https://gyazo.com/8743c8de9d348d7d000ee1c4f706a1eb.png)

下記コマンドどちらか入力します。

```bash
    #by npm
    npm i

    #by yarn
    yarn
```

すると、node_modulesがインストールされています。
もし、表示されていない場合は更新してみましょう。
![node_modules復活](https://gyazo.com/a98905dd6c4c776df42295b5e9e9f1f6.png)

:::message
インストールされているパッケージはyarn.lock(npmの場合はpackage-lock.json)をみて確認しています
:::

## 参考

[npmコマンドについて](https://docs.npmjs.com/cli/v7/commands/npm-install)
[yarnコマンドについて](https://classic.yarnpkg.com/en/docs/usage)
[yarn.lockについて](https://classic.yarnpkg.com/en/docs/yarn-lock/)