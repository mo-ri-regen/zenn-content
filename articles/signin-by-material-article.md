---
title: "(コピペでOK)material-uiで簡単にsigninページを作ってみた"
emoji: "👮🏽‍♀️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [React, materialui, デザイン, フロントエンド]
published: true
---

## 開発環境

@material-ui/core: ver 4.11.4
@material-ui/icons: ver 4.11.2
nextjs(未検証ですが、Reactでも動きます): ver 11.0.0

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

signin.jsをpagesディレクトリの直下に作ります。
そして、GitHubにある[SignIn.js](https://github.com/mui-org/material-ui/blob/master/docs/src/pages/getting-started/templates/sign-in/SignIn.js)をコピペします

![signin](https://gyazo.com/4d653a93c933f194c8b7e9f9dd6bd485.png)

コピペしただけで作れました🎉
あくまで、デザインだけなのでここからDBの連携やボタンを押したときの挙動など
機能面は別途作る必要があります。(ここでは省略します)

## リファクタリング

まず、拡張子がjsとなっているのでjsx(Typescriptの場合はtsx)にします
次に、コンポーネント化していきましょう
ソースコードみてるとcopyrightのところはコンポーネントとして扱えそうです。
![copyright](https://gyazo.com/2b83e26fd64e2ff23543d50ef7419efe.png)
なので、下記のようにディレクトリとファイルをそれぞれ作っていきましょう。
![ディレクトリ構成](https://gyazo.com/f244143de8d1f7a0cf744eea42945b07.png)

あとはcopyrightの'index.jsx'にcopyrightのところをコピペ(exportする必要はありますが)すればOK
![copyrightのコンポーネント化](https://gyazo.com/0721ac61717c054061eb498fa7530633.png)
signinページでimportするのも忘れないようにしましょう
![コンポーネントのimport](https://gyazo.com/409a278ed7c49a5c841771e41187396b.png)

他にも[テンプレート](https://material-ui.com/getting-started/templates/#react-templates)があるので興味があれば使ってみてください

## 参考

[github](https://github.com/mui-org/material-ui/tree/master/docs/src/pages/getting-started/templates/sign-in)

[テンプレート(公式ページ)](https://material-ui.com/getting-started/templates/#react-templates)
