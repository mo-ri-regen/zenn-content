---
title: "カスタムフックスの使い方"
emoji: "🧳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [React]
published: true
---

Reactでは自分でフックスを定義することでコンパクトに書くことができます。
また、コンポーネント間で同じフックスを使い回すことができます。

## 環境

React16.8以降

## 使い方

カスタムフックを定義するときは"use"で始まります。これは定義したフックスがフックスなのか関数なのか判断するためのルールです。
下記のような[フックスのルール](https://ja.reactjs.org/docs/hooks-rules.html)があります。
- return文より前に書きます。
- Reactの関数内で呼び出します。

## 使用例

```tsx
// useTextというカスタムフックスを定義する
const useText = () => {
  const [text, setText] = useState<string>("");
  const [list, setList] = useState<string[]>([]);

  const onChangeText = (e: React.ChangeEvent<HTMLInputElement>) => {
    setText(e.target.value);
  };
  return { text, list, onChangeText};
};  

  export default function Home() {

  const { text, list, onChangeText } = useText();

  return (
    // なんらかの処理
    // 呼び出すときはtext,list,onChangeTextをそれぞれそのまま呼び出します。
  )
```

カスタムフックスを導入したからといって、return文の中は特に変更を加えなくてもいいので変更は最小限で済みます。

## 参考

https://ja.reactjs.org/docs/hooks-custom.html

https://ja.reactjs.org/docs/hooks-rules.html
