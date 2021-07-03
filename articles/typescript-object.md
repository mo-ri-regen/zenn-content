---
title: "Typescriptを使ったオブジェクト型の定義方法"
emoji: "🏁" # 絵文字理由:defineの語源: finはfinish→Goal→🏁
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Typescript]
published: true
---

オブジェクト型で変数が定義されていたときに、typescript を使ってオブジェクト型ってどうやって指定するんだろう?🤔 と思い調べてみました。
結論、最初に"interface hoge" or "type hoge"という形で型を定義します。

```ts
// interfaceを使うときは下記のように定義
interface Person {
  name: string;
  age: number;
}

// typeを使うときは下記のように定義
type Person = {
  name: string;
  age: number;
}

// 関数で変数を定義するときは引数にオブジェクトの型を指定
function greet(person: Person) {
  return "Hello " + person.name;
}
```

cf.interface も type も使わないときは、下記のように直接指定して定義できます。
しかし、オブジェクトのプロパティの数が増えるとみづらくなるため interface or type を使った方がいいと思います。

```ts
function greet(person: { name: string; age: number }) {
  return "Hello " + person.name;
}
```

## type と interface どっちを使ったらいいのか問題

違いは公式の[文章](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)に書いてあるので時間があれば読んでみてください(~~まだ理解しきれていない~~)📚
調べていくと、zennでこのことに関して言及している[有益な記事](https://zenn.dev/seya/articles/aa94166c977280)を見つけました。
著者の見解ではどちらでも代用できるのであれば、typeのほうがいいだろうという見解でした。
[stackoverflow](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types)でも、話題に上がるような内容でした。
この内容を参考にして、今後は必要がなければ type だけを使った例で説明します。

## その他の使い方

- 「?」をつけると optional となって「?のプロパティ」を指定しなくてもエラーになりません。

```ts
type personalInfo = {
  name: string;
  height?: number;
  weight?: number;
}

// ? がついているプロパティは指定しなくてもエラーにならない!!
const person1:personalInfo = {name:'yamada'}
const person2:personalInfo = {name:'tanaka', height:170}
const person3:personalInfo = {name:'suzuki', weight:63}

// nameの値を指定していないためエラー
const person4:personalInfo = {height:181}
// personalInfoにないプロパティを指定しているためエラー
const person5:personalInfo = {name:'ikeda', age:32}
```

- readonlyで読み取り専用になる

```ts
type personalInfo = {
  readonly name: string;
  age:number;
}

const person1:personalInfo = {name:'yamada',age:36}

// 読み取り専用なので表示は可能
console.log(personal1.name)
// error 再代入は不可
person1.name = 'kimura'
// ageはreadonlyでないため再代入可能
person1.age = 45
```

:::message alert

readonly はエイリアス経由だと再代入可能になってしまうので注意。
(下記例を参照)
:::

```ts
type Person = {
  name: string;
  age: number;
}

type ReadonlyPerson = {
  readonly name: string;
  readonly age: number;
}

let writablePerson: Person = {
  name: "Person McPersonface",
  age: 42,
};

let readonlyPerson: ReadonlyPerson = writablePerson;

console.log(readonlyPerson.age); // prints '42'
// writableはreadonlyでないためエラーにならない!
writablePerson.age++;
// readonlyでも値が増えてしまう
console.log(readonlyPerson.age); // prints '43'
```

## 動作環境

下記環境で動くか確かめました。

[codesandbox](https://codesandbox.io/)

## 参考

[公式](https://www.typescriptlang.org/docs/handbook/2/objects.html)
[typeとinterfaceの違い](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)
[TypeScript で type と interface どっち使うのか問題](https://zenn.dev/seya/articles/aa94166c977280)
[stackoverflow](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types)
