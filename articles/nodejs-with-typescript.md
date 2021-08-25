---
title: "TypeScriptで書かれたJSをNode.js上で実行する方法"
emoji: "👻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [nodejs, typescript]
published: true
---

TypeScript で書かれている場合、一度 JS に変換(トランスパイル)してから 実行する必要があります。

1. TypeScript のインストール

   ```bash
   # npm
   npm i -D typescript

   # yarn
   yarn add typescript --dev
   ```

2. コンパイル

   下記コマンドを入力することで(エラーがなければ) hoge.js が生成されます。

   ```bash
   tsc hoge.ts
   ```

3. 実行

   hoge.js が作成されるので下記コマンドで実行できます。

   ```bash
   node hoge.js
   ```

## Deno との比較(感想)

過去に Deno を[触ってみました](https://zenn.dev/mo_ri_regen/articles/deno-helloworld-article)が Deno では、TypeScript に変換する必要がないので楽ですね。
そのうち、Node.js 使うなら Deno を使おうとなるかもしれません。

## 参考

https://nodejs.dev/learn/nodejs-with-typescript
