---
title: "Recoilのコア概念「AtomとSelector」について"
emoji: "👮"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Recoil,React]
published: true
---

## Recoilとは

Reactの状態管理ライブラリです
ちなみに他の状態管理として[Redux](https://redux.js.org/)などがあります。

## 最新バージョン

Recoil 0.4(2021/08/13時点)

## インストール方法

```bash
# npm
npm install recoil
# yarn
yarn add recoil
```

## Atom

Atomとは状態の単位です。Atomが更新されるとコンポーネントは再レンダリングされます。
同じAtomが複数のコンポーネントで使われるとき、すべてのコンポーネントがそのAtomを共有します。

### 使い方

atom関数を使って定義できます。
keyの値はユニークである必要があります。

```js
const fontSizeState = atom({
  key: 'fontSizeState',
  default: 14,
});
```

ReactのuseStateと同じような書き方で、useRecoilStateをRecoilでは使います。
useStateとの違いはコンポーネント間で状態が共有されるところです。

```js
function FontButton() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  return (
    <button onClick={() => setFontSize((size) => size + 1)} style={{fontSize}}>
      Click to Enlarge
    </button>
  );
}

// 別コンポーネントで状態が共有されるためボタンをクリックすると
// FontButtonのfontSizeと下記TextのfontSizeは同じになる
function Text() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  return <p style={{fontSize}}>This text will increase in size too.</p>;
}
```

## Selector

selectorはatomまたは他のselectorを入力として受け取る関数で、同期的または非同期的に状態を変化させます。入力として受け取ったatom、または入力として受け取ったselectorが更新されるとselectorは再計算されます。また、selectorが変わったときに再レンダリングされます。
getプロパティの引数を使ってatomと他のselectorにアクセスできます。
下記の例ではfontSizeStateというatomを入力として受け取っています。

```js
const fontSizeLabelState = selector({
  key: 'fontSizeLabelState',
  get: ({get}) => {
    // fontSizeStateがatomとなる
    const fontSize = get(fontSizeState);
    const unit = 'px';

    return `${fontSize}${unit}`;
  },
});
```

### 値の読み取り方法

useRecoilValue()を使うことで値の読み取りを行うことができます。

```js
function FontButton() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  const fontSizeLabel = useRecoilValue(fontSizeLabelState);

  return (
    <>
      <div>Current font size: {fontSizeLabel}</div>

      <button onClick={() => setFontSize(fontSize + 1)} style={{fontSize}}>
        Click to Enlarge
      </button>
    </>
  );
}
```

詳しくは書きませんが[atom](https://recoiljs.org/docs/api-reference/core/atom)と[selector](https://recoiljs.org/docs/api-reference/core/selector)にはそれぞれ使えるAPIがあります。

## TypeScript

[公式](https://recoiljs.org/blog/2020/06/18/0.0.10-released/#typescript-support)に記載の通り、TypeScriptのサポートはされているようですが、使い方は現時点ではよくわかりませんでした🙇‍♀️
[GitHub](https://github.com/facebookexperimental/Recoil)をみるとTypeScriptの使用率が2.2%^[2021/08/13時点]なところからまだまだこれからなのかなと思います
![Recoilの言語の割合](https://gyazo.com/dd552c63e1be88940c5eac41c920eb8a.png)
*Recoilの言語の割合*

## 参考

https://recoiljs.org/
