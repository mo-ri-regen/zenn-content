---
title: "Set関数でユニークな値のみ格納する"
emoji: "👨‍👩‍👧‍👦"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [js, ECMAScript]
published: true
---

## 使い方

Set 関数を使うと一意の値を格納します。
大文字と小文字は区別されるため、大文字、小文字を区別せずに一意の値を格納したい場合は
Set 関数を使う前に、操作する配列について大文字に統一するまたは小文字に統一する必要があります。

例

```js
// ex1
const array = [1, 3, 2, 5, 2, 4, 1, 8, 4];

const uniqueArray = [...new Set(array)]; // [1, 3, 2, 5, 4, 8]

// ex2
new Set("Firefox"); // Set(7) [ "F", "i", "r", "e", "f", "o", "x" ]
new Set("firefox"); // Set(6) [ "f", "i", "r", "e", "o", "x" ]
```

## 対応ブラウザ

[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Set)によると IE 以外のブラウザはサポートされています。

## 参考

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Set

https://spyweb.media/2017/12/22/js-remove-array-duplicates/
