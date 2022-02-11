---
title: "Next.jsとTailwindCSSでフッターにRemixIconを配置する"
emoji: "🍱"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [remixicon, nextjs, tailwindcss, アイコン]
published: true
---

## RemixIcon について

Remix アイコンは[Apache License Version 2.0](https://github.com/Remix-Design/remixicon/blob/master/License)をもつオープンソースで提供されており、2200 以上[^1]のアイコンがあります。
個人利用はもちろん商用利用可能であり、 24px\*24px の svg 形式としてダウンロードすることもできますが、クラス名を指定して使用することもできます。
今回はアイコンをクリックするとページ遷移するように実装したいと思います。

[^1]: 2022/02/11 時点

## 環境

- Next.js ver 12
- remixicon ver 2.5.0
- TailwindCSS ver 3.0.17

## 使用法

[公式サイト](https://remixicon.com/)から使いたいアイコンを探します。
今回は Twitter のアイコンと GitHub のアイコンを使いました。
svg 形式でダウンロードできますが今回はクラスを使います。

![Twitterアイコンの検索](https://gyazo.com/274dc41362eed4863bfebd4257e64467.png=20x)

クラス名は"ri-{アイコン名}-{サイズ}"という規則で付けられています。
画像では class を使っていますが、Next.js なので className を使います。

### インストール

公式では npm を使っていますが、yarn で RemixIcon をインストールします。

```bash
yarn add remixicon
```

### ソースコード

#### フッター部分

下記 2 行を加えるだけでアイコンを利用できます。

```tsx
import "remixicon/fonts/remixicon.css";
<i className="ri-twitter-fill"></i>;
```

今回は最下部に固定で配置させたいので

```tsx
className = "absolute inset-x-0 bottom-0";
```

で固定させています。
また、ページ遷移させたいので Link タグを使っています。

```tsx:src/component/layout/container/footer.tsx
import type { NextPage } from "next";
import Link from "next/link";
import "remixicon/fonts/remixicon.css";
export const Footer = () => {
  return (
    // 最下部に固定で配置
    <div className="absolute inset-x-0 bottom-0 h-8 bg-green-200">
      {/* 中央に配置 */}
      <footer className="flex justify-center gap-x-4">
        <Link href="https://twitter.com/{TwitterName}">
          <a>
            {/* アイコンをセットする */}
            <i className="ri-twitter-fill"></i>
          </a>
        </Link>
        <Link href="https://github.com/{GitHubName}">
          <a>
            {/* アイコンをセットする */}
            <i className="ri-github-fill"></i>
          </a>
        </Link>
      </footer>
    </div>
  );
};

```

#### 呼び出し側

```tsx:src/pages/index.tsx
import type { NextPage } from "next";
import Head from "next/head";
import { Footer } from "../component/layout/container/footer";

const Home: NextPage = () => {
  return (
    <div>
      <Head>
        <title>タイトル</title>
        <meta name="description" content="title" />
      </Head>
      {/* コンポーネントを呼び出し */}
      <Footer />
    </div>
  );
};

export default Home;
```

## 実行結果

![実行結果](https://gyazo.com/3245754a92502abf60d2a6acf21974d0.png=20x)

フッター部分にアイコンをつけることができました。

## 最後に

> We would be very grateful if you mention "Remix Icon" in your product info, but it's not required.

とあるので感謝の意味を込めて ReadMe.md などに Remix Icon を使用したことを記載すると開発者に喜ばれるかもしれません。

## 参考

- 公式
  [Remix Icon](https://github.com/Remix-Design/remixicon)
- Tips
  [Nextjs でページ遷移させる方法](https://nextjs.org/docs/api-reference/next/link)
  [Tailwind CSS で下部に配置する方法](https://tailwindcss.com/docs/top-right-bottom-left)
