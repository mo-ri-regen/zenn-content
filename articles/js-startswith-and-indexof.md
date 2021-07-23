---
title: "startsWithとincludesの使い方"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [javascript]
published: true
---

startsWithを使うと前方一致しているかどうかを判定することができます。
includesを使うと文字が含まれているかどうかを判定することができます。

## startsWithについて

### 構文

> str.startsWith(searchString[, position])

strが(positon+1)文字目のsearchStringから始まっているかどうかを判定します。
positon:省略可能。既定値は0。数字を指定します。
ECMAScript2015から追加されました。

### 返送値

大文字・小文字は区別されます。
指定された文字で始まっているときtrue。
そうでなければfalse。

### 使い方

```js

let str = 'To be, or not to be, that is the question.'

console.log(str.startsWith('To be'))          // true
console.log(str.startsWith('not to be'))      // false
console.log(str.startsWith('not to be', 10))  // true
```

### ブラウザのサポート

IE以外はサポートされています🎉
IEはサポート切れるので無視していいのかなと思います。

---

## includesについて

### 構文

> str.includes(searchString[, position])

startsWithと同様にECMAScript2015から追加されました。

### 返送値

大文字・小文字はそれぞれ区別されます。
(positon+1)文字目以降でstrがsearchStringを含んでいればtrue。
そうでなければfalse。

### 使い方

```js
const str = 'To be, or not to be, that is the question.'

console.log(str.includes('To be'))        // true
console.log(str.includes('question'))     // true
console.log(str.includes('nonexistent'))  // false
console.log(str.includes('To be', 1))     // false
console.log(str.includes('TO BE'))        // false
console.log(str.includes(''))             // true

```

### ブラウザのサポート

こちらもIE以外はサポートされています🎉

## 参考

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/includes