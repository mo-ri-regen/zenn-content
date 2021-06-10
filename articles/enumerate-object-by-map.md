---
title: "map関数を使ったオブジェクトの要素の列挙"
emoji: "👼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [javascript,ECMAScript,オブジェクト,map関数]
published: true
---

オブジェクトの要素を列挙するには、どうしたらいいのか調べてみたら
配列の要素を列挙するときにも使ったmap関数を使えばよいことがわかったので
使い方をまとめてみた。

## 構文

Object.Keysとmapを組み合わせることで
オブジェクトの要素を取り出すことができる

```js
Object.keys({オブジェクト名}.map((piyo)=>{
  //何かしらの処理
}))
```

## 例

```js
const hoge = {
  "a":1,
  "b":2,
  "c":3
}

Object.keys(hoge).map((key)=>{
  console.log(`${key}:${hoge[key]}`)
})

// 出力結果
// "a:1"
// "b:2"
// "c:3"
```

オブジェクトの値が配列のときも同様の処理で要素が取得可能。

```js
const fuga = {
  "a":["a1","a2","a3"],
  "b":["b1","b2","b3"],
  "c":["c1","c2","c3"]
};

Object.keys(fuga).map((key)=>{
  console.log(`${key}:${fuga[key]}`)
})

// 出力結果
// "a:a1,a2,a3"
// "b:b1,b2,b3"
// "c:c1,c2,c3"
```

:::details map関数以外で要素を列挙する方法

mapのかわりにforEachを使っても同様の処理が行える。

```js
const fuga = {
  "a":["a1","a2","a3"],
  "b":["b1","b2","b3"],
  "c":["c1","c2","c3"]
};

Object.keys(fuga).forEach((key)=>{
  console.log(`${key}:${fuga[key]}`)
})

// 出力結果
// "a:a1,a2,a3"
// "b:b1,b2,b3"
// "c:c1,c2,c3"
```

:::

## 注意(for ... inについて)

for ... inを使ってもオブジェクトの値を取得可能だが、
親オブジェクトまで探索してしまい、意図しない結果になりうるので
使うべきでない。

:::details for ... in の構文

```js
for ({プロパティ} in {オブジェクト}) {
  //何らかの処理
}
```

:::

## 実行環境

[JSfiddle](https://jsfiddle.net/)

## 参考URL

[JavaScript Primer 迷わないための入門書(ループと反復処理)](https://jsprimer.net/basic/loop/)