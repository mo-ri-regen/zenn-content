---
title: "yarnでパッケージをアンインストールする方法"
emoji: "😸"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [yarn]
published: true
---

## アンインストール方法

```bash
yarn remove <package>　--<flag>
```

yarn install と同じ flag を使うことができます。(flag はなくても問題ないです。)
package.json と yarn.lock がそれぞれアップデートされ、package が削除されます。
未検証ですが、他の開発者は"yarn install"を使えば node_modules が同期されるそうです。
package を削除すると dependencies, devDependencies などの依存関係から削除されます。

## 具体例

[SWR](https://swr.vercel.app/ja)をアンインストールしたいとき

```bash
yarn remove swr
```

## 参考

https://classic.yarnpkg.com/en/docs/cli/remove/
