---
title: "jsの??をみて頭の中は??にならないために"
emoji: "🤔"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [javascript,ECMAScript]
published: true
---

ES2020の構文で??をみたときに頭の中が??になったので使い方を勉強しました。

## Nullish Coalescing Operator(??演算子について)

### 構文

```js
leftExpr ?? rightExpr
```

### 使い方

```js
const y = null;
const z = 2;
const x = y ?? z;
console.log(x); // 2

const y = 6;
const z = null;
const x = y ?? z;
console.log(x); // 6

const y = undefined;
const z = null;
const x = y ?? z;
console.log(x); // null

const y = null;
const z = undefined;
const x = y ?? z;
console.log(x); // undefined
```

MDNによると

```js
leftExpr ?? rightExpr
```

について
> 左辺が null または undefined の場合に右の値を返し、それ以外の場合に左の値を返します。

と書かれています。codesandboxで実験してみると??はnullまたはundefinedでないほうをzに返しているようです。
(実際にはyの値を評価してyがnullまたはyがundefinedだったらzを返すというような書き方をすると思いますが😅)
優先順位としてはyの値を評価→yがnullまたはyがundefindedならzの値を評価という順番のようです。

## ??=演算子について

これは「??」と代入の「=」を組み合わせた演算子です。

### 構文

```js
expr1 ??= expr2
```

### 使い方

```js
let y = 3;
const z = 5;
y ??= z;
console.log(y); // 3

let y = null;
const z = 5;
y ??= z;
console.log(y); // 5
```

??=は下記の式と等価です。

```js
x ?? (x = y);
```

つまり、xがnullでないまたはxがundefinedでないならyの値をxに代入するということです。

:::message alert
常に代入が行われる下記とは等価ではありません

```js
x = x ?? y;
```

:::
## Optional Chaining(?.について)

### 使い方

```js
const object = {
  property: {
    property: {
      property: "value"
    }
  }
}
 
if (object?.property?.property?.property) {
  object.property.property.property = "new value";
}
```

"?."はnullまたはundefinedのときundefinedを返します。
ネストされたオブジェクトの値を調べるときに役立ちます。

## その他

他の?の構文として三項演算子があると思います。
[この記事](https://zenn.dev/mo_ri_regen/articles/ternary-expression)でpythonをjsの比較をしながら三項演算子の書き方を調べました。

## 参考

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Logical_nullish_assignment

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Optional_chaining

https://mcro.tech/blog/es2020/

https://zenn.dev/tonkotsuboy_com/articles/es2021-whats-new

