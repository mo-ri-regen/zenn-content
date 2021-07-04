---
title: "Next.jsの環境変数取得方法"
emoji: "🐷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [nextjs]
published: false
---

Nextjsでは、たとえばデータベースに接続するときに使う環境変数を設定することができます。
設定方法は、ルートディレクトリ直下にあるnext.config.jsにあるmodule.exports...とあるところに変数を追加すればOKです。(ファイルがなければnext.config.jsをルート直下に作ってください)

```js:next.config.js
module.exports = {
  env: {
    // customKeyは任意の変数名でOK
    // 'my-value'のところで値を設定する
    customKey: 'my-value',  
  },
};
```

:::message
ターミナル上で下記メッセージ

>Found a change in next.config.js. Restart the server to see the changes in effect.

が出た場合は

```bash
yarn dev  # or npm run dev
```

を使ってサーバを再起動します。
:::

値を取得する場合は下記のようにprocess.envを使います。
(customKeyのところは設定した変数名に変えてください。)

```jsx:hoge.jsx
return <h1>The value of customKey is: {process.env.customKey}</h1>
```

## 動作環境

Nextjs 9.4以降(11.0.0で動作確認済み)

## 参考 URL

[環境変数について](https://nextjs.org/docs/api-reference/next.config.js/environment-variables)

[next.config.jsについて](https://nextjs.org/docs/api-reference/next.config.js/introduction)
