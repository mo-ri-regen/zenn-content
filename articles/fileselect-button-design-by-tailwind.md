---
title: "tailwindでファイル選択ダイアログのデザイン変更"
emoji: "👩‍🎨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [tailwindcss,html]
published: true
---

ローカルのファイルを選択するときにinput type=fileを使う人もいると思いますが、classを指定してもデフォルトだと画像のようにファイル選択するボタンのデザインをカスタマイズできません。なので、ボタンの文字の変更をしたいと思ってもできません。

```html
<input type="file" class="p-6 bg-red-500" />
```

![inputタグのデフォルトデザイン](https://gyazo.com/363d5aea65f28f478c817245f4a76276.png)

## デザイン変更

tailwindを使ってデザインを変えていこうと思います。下記操作を行えばデザインの変更ができます。
1. labelタグでinputタグを囲みます。
2. labelタグとinputタグの間に表示させたい文字を入力します。
3. inputタグのclassはhiddenにしてlabelタグのclassにデザインを指定します。
```html
<label class="p-6 bg-red-500">
  ファイル選択
  <input class="hidden" type="file" />
</label> 
```

![デザイン変更](https://gyazo.com/d79b33c2afa1d36ac1187ab1bdaac2ca.png)

無事、デザインが変わりました🎉
tailwindでデザイン変える方法は勉強中なので、いろいろ触ってみようと思います。

## 実行環境

https://play.tailwindcss.com/

## 参考

https://proengineer.internous.co.jp/content/columnfeature/7605
