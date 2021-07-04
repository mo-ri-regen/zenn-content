---
title: "Next.jsの環境変数取得方法"
emoji: "🐷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [nextjs]
published: false
---

Nextjsでは、たとえばデータベースに接続するときに使う環境変数を設定することができます。
設定方法は、nextjs.config.jsにあるmodule.exports...とあるところに変数を追加すればOKです。

```js
module.exports = {
  env: {
    customKey: 'my-value',
  },
};
```

値を取得する場合は下記のようにprocess.envを使います。

```jsx
return <h1>The value of customKey is: {process.env.customKey}</h1>
```

## 動作環境

Nextjs 9.4以降

## 参考 URL

[nextjs公式](https://nextjs.org/docs/api-reference/next.config.js/environment-variables)
