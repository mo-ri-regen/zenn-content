---
title: "Recoilのコア概念「AtomとSelector」について"
emoji: "👮"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Recoil]
published: false
---

## Recoilとは

Reactの状態管理ライブラリです
他の状態管理として[Redux](https://redux.js.org/)があります。

## バージョン

Recoil 0.4

## インストール方法

```bash
# npm
npm install recoil
# yarn
yarn add recoil
```

## Atom

Atomとは状態の単位。Atomが更新されるとコンポーネントは再レンダリングされる。
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

Selectorは関数で同期的または非同期的に状態を変化させます。

```js
const fontSizeLabelState = selector({
  key: 'fontSizeLabelState',
  get: ({get}) => {
    const fontSize = get(fontSizeState);
    const unit = 'px';

    return `${fontSize}${unit}`;
  },
});
```

## TypeScript

[公式](https://recoiljs.org/blog/2020/06/18/0.0.10-released/#typescript-support)に記載の通り、TypeScriptのサポートはされているようですが、使い方は現時点ではよくわかりませんでした。


## 参考

https://recoiljs.org/
