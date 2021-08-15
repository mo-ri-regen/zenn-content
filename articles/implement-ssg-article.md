---
title: "【簡単】Next.jsによるSSGの実装"
emoji: "🏰"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [nextjs,ssg]
published: true
---

Next.jsではAPIを叩くときにgetStaticPropsを使うことで、ビルド時にデータを取得して事前にHTMLファイルのレンダリングを行うことができます。ビルド時にデータを取得して事前にHTMLファイルのレンダリングを行うことを**SSG**と呼びます。
TypeScriptを使う場合はgetStaticPropsの型にGetStaticProps^[TypeScriptのときはGetStaticPropsをimportする必要がある]を指定します。

:::details SSG(StaticSiteGeneration)とは
Static Generationと呼ばれることもあります。
ビルド時にデータを取得することでpre-renderされるため高速にデータを読むことができます。
リアルタイム性が要求される場面では、SSRを使ってリクエストがあるたびにデータを読み込むなど工夫が必要です。

[WebDBVol123で学んだこと](https://zenn.dev/mo_ri_regen/articles/webdb-vol123)でもSSR,SSG,CSRについて書いたのでよろしければお読みください。
:::

:::message
SSGの挙動をするにはリリース環境で動作させる必要があります。(後述の注意点参照)
:::

## 使い方

```tsx
import { GetStaticProps } from 'next'

export const getStaticProps: GetStaticProps = async() => {
// export async function getStaticProps() でも同じ
  const res = await fetch(`https://.../data`)
  const posts = await res.json()

  if (!posts) {
    return {
      notFound: true,
    }
  }

  return {
    props: { posts }, // will be passed to the page component as props
  }
}
```

getStaticPropsでreturnされたpropsを関数側の引数に渡すことができます。

```tsx
import { GetStaticProps } from 'next'

// posts will be populated at build time by getStaticProps()
function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}

export const getStaticProps: GetStaticProps = async() => {
    // 最初の例と同じなので省略

    return {
        props: { posts }, // will be passed to the page component as props
    }
}
```

## getStaticPropsの注意点

- オブジェクトを返すようにします。
notFoundを指定すると404を返すことを許可するか設定できます。
その他、リダイレクトの設定などできます。
- "pages/*"からしかexportできません。
- コンポーネントとして定義してはいけません。
- 開発環境(yarn devを行なったとき)ではリクエストがあるたびにgetStaticPropsが呼ばれます。

## 動作環境

ver 9.3.0以降
(notFoundOptionはver10.0.0以降)

## 参考

https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation

https://blog.logrocket.com/ssg-vs-ssr-in-next-js/
