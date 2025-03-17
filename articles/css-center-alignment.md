---
title: "marginを使って中央揃えできなかったときの対処法"
emoji: "🎨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [HTML, CSS]
published: true
---

## はじめに

CSS で margin を使ったときに中央揃えができなかったときに調べたことを記載しました。

- 修正前のソースコード

```css
div {
  margin: 0 auto;
  background-color: yellow;
}
```

![CSS修正前](https://storage.googleapis.com/zenn-user-upload/cd2d100e46a5-20250317.jpg)

## 原因

margin:0 auto;を使ったときに中央揃えできないときは下記を確認します。

- **ブロックレベル**の要素に対して指定しているか
- width の指定をしているか

margin はブロックレベルの要素に対して指定するが、ブロックレベルだとデフォルトで width は 100%となっているため親要素の幅いっぱいに広がっています。width を指定することで(親要素の幅 - 要素の幅)が左右にできるため auto で左右の余白を均等に分配され、中央に配置されます。

- ソースコード

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="styles.css" />
    <title>Document</title>
  </head>
  <body>
    <div>text1</div>
  </body>
</html>
```

```css
div {
  margin: 0 auto;
  width: fit-content; /*コンテンツのサイズに基づいて適切な幅を指定*/
  background-color: yellow;
}
```

![CSS修正後](https://storage.googleapis.com/zenn-user-upload/510aa58fff46-20250317.jpg)
