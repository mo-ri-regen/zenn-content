---
title: "リセットcssによるブラウザ特有のCSSの打ち消し"
emoji: "☝️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [css]
published: false
---

## リセットCSSとは

デフォルトでは、特に何も設定していなくてもブラウザごとにスタイルシートが定義されてます。
そのスタイルシートを打ち消すためのスタイルシートを**リセットCSS**と呼びます。
リセットCSSを読み込むことでブラウザごとの差をなくすことができます。

:::message
cf. 似た概念としてnormalize.cssというのもあります。こちらはブラウザごとの差異をなくすということは共通していますが、異なる点はブラウザ特有のCSSをなくすということは行なっていないという点です。
:::

## 使い方

リセットCSSを定義してから通常のCSSを定義します。古いものもあるため注意が必要です。
(リセットCSSを後で定義してしまうとリセットCSSで上書きされてしまうため。)

:::message alert
コピペするときはライセンスに気をつけましょう。
:::

```html
<head>
  <link rel="stylesheet" href="reset.css">
  <link rel="stylesheet" href="style.css">
</head>
```

## 例

自分でリセットCSSを定義してもいいのですが、すでに定義されたCSSがあるのでそれを読み込むのが簡単です。[coliss](https://coliss.com/articles/build-websites/operation/css/css-reset-for-modern-browser.html)のところに定義されてある[ソースコード](https://github.com/andy-piccalilli/modern-css-reset/blob/master/dist/reset.min.css)をコピペしてくるのが一番楽かなと思います。

## リセットCSSを使ってみた

GoogleChromeとfirefoxをそれぞれ使ってリセットCSS適用前後の比較をしてみました。
スペースの間隔がみやすいように背景だけ変更しています。

### 適用前

- chrome
![リセットCSS適用前(chrome)](https://gyazo.com/0c74dc6cd90d1b33586f946322cd5665.png)

- firefox
![リセットCSS適用前(firefox)](https://gyazo.com/3f67fce7949ba071a0146039a7db5cda.png)

例が悪いのかchromeとfirefoxの違い自体はよくわからなかったですが、それぞれh1とh2の間にスペースがあるなどのブラウザ特有のCSSが適用されています。

### 適用後

- chrome
![リセットCSS適用後(chrome)](https://gyazo.com/a43b9d765dbd24086ce660654e29e5c8.png)

- firefox
![リセットCSS適用後(firefox)](https://gyazo.com/71ebb7262b663963c8cdedee2d9a4f51.png)

リセットすることで、間隔が詰まって表示することができるようになりました。

cf. ソースコード

```html

<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="reset.css" />
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <h1>h1</h1>
    <h2>h2</h2>
    <input type="text" />
    <div>div</div>
  </body>
</html>

```

## 参考

[リセットCSS](https://coliss.com/articles/build-websites/operation/css/css-reset-for-modern-browser.html)

[リセットCSS(ソース)](https://github.com/andy-piccalilli/modern-css-reset/blob/master/dist/reset.min.css)
