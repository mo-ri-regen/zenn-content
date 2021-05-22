---
title: "pythonとjavascriptの三項演算子の比較"
emoji: "⚖️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [javascript, python3,三項演算子]
published: true
---

pythonで三項演算子の書き方を調べてみたらjsと全然書き方違っていたので、
それぞれの書き方を比較してみました⚖️
参考までに三項演算子を使わないパターンも最後に書いてます。

## 構文

構文は下記の通りです。
文章だけだとわかりづらいと思うのでソースコードも参照してください。

- python

{条件式が真の場合} if {条件式} else {条件式が偽の場合}

- javascript

{条件式} ? {条件式が真の場合}:{条件式が偽の場合}

## ソースコード

### 三項演算子を使う場合

- python

```python3:test.py
a,b=3,5

result = 2*a if a>b else 2*b
print(result)
# 実行結果: 10
```

- javascript

```js:test.js
const a=3,b=5

const result = a>b ? 2*a : 2*b
console.log(result)
// 実行結果: 10
```

### 参考(三項演算子を使わない場合)

- python

```python:test.py
a,b=3,5

if a>b:
    result = 2*a
else:
    result = 2*b

print(result)
# 実行結果: 10
```

- javascript

```js:test.js
const result = (a,b) => {
    if (a > b){
        return 2*a;
    }
    else{
        return 2*b;
    }
};

console.log(result(3,5));
// 実行結果: 10
```

## 比較

- 理解のしやすさ

jsと比べてpythonのほうがif文で書いているので
わかりやすいです😊
三項演算子をjsで初めてみたときは、"?"がついていて自分の頭の中が「???」になったのを
思い出しました。

- 可読性

jsのほうが 条件比較、trueの場合、falseの場合と
左から右へ読むので読みやすいです。
pythonの場合は条件式が真ん中にあるので少し読みづらく感じました。

- 三項演算子を使った場合と三項演算子を使わなかった場合

pythonもjsも三項演算子を使わない場合、どちらも行数が増えました😲
さらにjsは(constを使おうとしたからというのもありますが)
少し複雑になりましたね。
シンプルに書こうと思うと三項演算子の書き方はマスターしたほうがいいと改めて思いました。

## 実行環境

[paiza.io](https://paiza.io/help)で動作確認しました👀

- Python
ver 3.8.5

- javascript
Node.js v14.15.4