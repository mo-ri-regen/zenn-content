---
title: "(コピペでOK)material-uiで簡単にsigninページを作ってみた"
emoji: "💄"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [React, デザイン, フロントエンド, materialui]
published: false
---

## インストール

npmもしくはyarnを使ってインストールしましょう

    ```bash
    // with npm
    npm install @material-ui/core
    npm install @material-ui/icons

    // with yarn
    yarn add @material-ui/core
    yarn add @material-ui/icons
    ```

## signinページ

GitHubにあるSignIn.jsをコピペします

![signin](https://gyazo.com/4d653a93c933f194c8b7e9f9dd6bd485.png)

コピペしただけで作れました🎉

## リファクタリング

コンポーネント化していきましょう

## 参考

[github](https://github.com/mui-org/material-ui/tree/master/docs/src/pages/getting-started/templates/sign-in)