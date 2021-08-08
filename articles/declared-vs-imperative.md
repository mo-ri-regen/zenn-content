---
title: "宣言型プログラミングと命令型プログラミング"
emoji: "👩🏼‍💻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [宣言型プログラミング,命令型プログラミング]
published: true
---

## TL;DR

宣言型プログラミングのほうが命令型プログラミングより読みやすいです
ReactやVueなど宣言型で記述されています📝

## 宣言型プログラミング(Declarative Programming)とは

何をするのか(What)を記述するプログラミング言語です。
具体的な処理はメソッドによって抽象化されて隠蔽されるので、読むときはメソッドの名前を見ると何をしているのかわかりやすいです。React,Vueは宣言的に記述できます。

### 具体例

Reactで宣言的に書くと次のようになります。
HTMLが視覚的に表示されているためわかりやすいです。

```js
const { render } = ReactDOM;
const Welcome = () => ( 
    <div id="welcome">
        <h1>Hello World</h1>
    </div>
);

render(<Welcome />, document.getElementById("target"));
```

## 命令型プログラミング(Imperative Programming)

結果を得るための手順(How)を記述するプログラミング言語です。
処理を一つずつ書く必要があるためコメントがないと可読性が下がります。

### 具体例

素のjsで命令的に書くと次のようになります。
DOM操作をしていますが、ぱっと見何をしているかわかりづらいです。

```js
const target = document.getElementById("target");
const wrapper = document.createElement("div");
const headline = document.createElement("h1");
wrapper.id = "welcome";
headline.innerText = "Hello World";
wrapper.appendChild(headline);
target.appendChild(wrapper);
```

:::message
素のjsでも宣言的に書くことは可能です。
詳しくは[参考書籍](https://www.oreilly.co.jp/books/9784873119380/)をご覧ください📚
:::

## 参考

[Alex Banks、Eve Porcello 著『React ハンズオンラーニング 第 2 版』(オライリー・ジャパン発行)](https://www.oreilly.co.jp/books/9784873119380/)
