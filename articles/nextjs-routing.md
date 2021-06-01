---
title: "nextjsのルーティング"
emoji: "🛣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Nextjs, Linkコンポーネント, フロントエンド]
published: true
---

## pagesディレクトリについて

Next.jsではpagesディレクトリの直下に'index'という名前のファイルを配置すると、
自動的にルートディレクトリとみなされる。
なので呼び出すときは「'/'」だけでよい

ex. 

- 'pages/index.js'→'/'

- 'pages/blog/index.js'→'/blog'

## ネスト

'index'という名前以外を使うと、呼び出すときは拡張子を除いたpagesからの
相対パスを指定する。

ex. 

- 'pages/blog/first-post.js'→'/blog/first-post'

- 'pages/dashboard/settings/username.js'→'/dashboard/settings/username'

## Linkについて

jsでは<a>タグを使ってページ遷移を行うことができるが、Next.jsではLinkコンポーネントを使って
ページ遷移を行うことができる。Linkコンポーネントを使うときは<a>タグを内部におく。(下記ソースコード参照)
また、Linkコンポーネントは<a>タグと比べて高速である。なぜなら、<a>タグを使うとリロードされてしまうからである。

[公式チュートリアル](https://nextjs.org/learn/basics/navigate-between-pages/client-side)を見てわかるように<a>タグを使うとリロードされてしまうため、ページ遷移後に色が元の色に戻ってしまう。

## 使い方
```js:Home.jsx
import Link from 'next/link'

function Home(){
  return(
    <li>
      <Link href='/'>
        <a>pages/index.jsxに遷移する</a>
      </Link>
    <li>
    <li>
      <Link href='/about'>
        <a>pages/about.jsxに遷移する</a>
      </Link>
    <li>
    <li>
      <Link href='/blog/hello-world'>
        <a>pages/blog/hello-world.jsxに遷移する</a>
      </Link>
    <li>
  );

}
```
## 参考

[公式サイト](https://nextjs.org/docs/routing/introduction)
[Linkコンポーネントについて](https://nextjs.org/learn/basics/navigate-between-pages/link-component)
[ページ遷移の話](https://nextjs.org/learn/basics/navigate-between-pages/client-side)