---
title: "Nextjsにtailwindcssをインストールしてみる"
emoji: "🎭"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [tailwindcss,nextjs]
published: true
---

Nextjsにtailwindcssを入れてから実際に使えるようにするまでの流れをみていきます。
公式ではnpmを使っているのでyarnでインストールしていこうと思います。

## 前提

Node.js 12.13.0以降をインストールしている

## インストール方法

1. インストール
  
    ターミナルを開いて下記のように入力します。
    ```bash
    yarn add -D tailwindcss@latest postcss@latest autoprefixer@latest
    ```

  

2. tailwind.config.js と postcss.config.jsの作成
  
    ```bash
    npx tailwindcss init -p
    ```

    上記、コマンドを打つと下記のように最小限の設定がされたtailwind.config.jsとpostcss.config.jsがそれぞれ生成されています。
    ```js:tailwind.config.js
    module.exports = {
      purge: [],
      darkMode: false, // or 'media' or 'class'
      theme: {
        extend: {},
      },
      variants: {
        extend: {},
      },
      plugins: [],
    }
    ```

    ```js:postcss.config.js
      module.exports = {
        plugins: {
          tailwindcss: {},
          autoprefixer: {},
        },
      }
    ```

## 初期設定

下記のようにpurgeを設定します。
(ディレクトリの構成に応じてパスは変えてください。)

```diff js:tailwind.config.js
- purge: [],
+ purge: ['./pages/**/*.{js,ts,jsx,tsx}', './components/**/*.{js,ts,jsx,tsx}'],
```

## 導入

導入方法は2つあります。
公式では「cssにimportする」をベストプラクティスとしています。

- jsに直接importする

pages/_app.js内に下記のように記述します。

```diff js:pages/_app.js
- import '../styles/globals.css'
+ import 'tailwindcss/tailwind.css'
```

この方法を使うときはNext.jsを作成したときに存在するglobals.cssとHome.module.cssをそれぞれ削除しても問題ありません。

- cssにimportする

./styles/globals.cssで下記のように設定をして、pages/_app.jsでimportしておきます。

```css:./styles/globals.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```js:pages/_app.js
import '../styles/globals.css'

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default MyApp
```

## 再起動

設定が終わったら下記コマンドで再起動しましょう。

```bash
yarn dev
```

## 完成

設定が終わったら[公式ドキュメント](https://tailwindcss.com/docs)を参考にサイトをデザインしていきましょう👩‍🎨

## 参考

https://tailwindcss.com/docs/guides/nextjs
