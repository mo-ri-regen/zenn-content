---
title: "ReactのdangerouslySetInnerHTMLの危険性"
emoji: "👮‍♂️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [react, セキュリティ, xss]
published: true
---

React では innerHTML の代替として dangerouslySetInnerHTML を使うことができます。
\_\_html をキーとして持つオブジェクト[^1]を渡す必要があります。

:::message alert
この関数は HTML をそのまま出力するので XSS 攻撃される危険性[^2]があります。
XSS については[過去記事](https://zenn.dev/mo_ri_regen/articles/cross-site-scripting)で書いたので、よければどうぞ 👋
:::

[^1]: 直接 HTML を触るので、危険であることを明示的に示すためです。
[^2]: 今回の攻撃は Dom 操作による XSS 攻撃のため、Dom-based XSS と呼ばれます。

## 使い方

```jsx
export default function App() {
  const createMarkup = () => {
    return { __html: "First &middot; Second" };
  };

  return <div dangerouslySetInnerHTML={createMarkup()} />;
}
```

## 何が dangerously か

下記のように意図しないスクリプトを埋め込むことができます。

```jsx
export default function App() {
  const createMarkup = () => {
    return {__html: '<script>alert('1')</script>'};
  }

  return (
    <div dangerouslySetInnerHTML={createMarkup()} />
  );
}
```

## その他

Vue,Angular でも下記関数を使うと攻撃される恐れがあるので気をつけましょう。

### Vue

- v-html ディレクティブ
- render 関数における domProps や domPropsInnerHtml

### Angular

- (1.x 系)ng-bind-html ディレクティブ
- (2.0 以降)DomSanitizer.bypassSecurityTrustHtml

## 参考

[詳解セキュリティコンテスト CTF で学ぶ脆弱性攻略の技術](https://book.mynavi.jp/ec/products/detail/id=122750)
[公式ドキュメント](https://ja.reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml)
