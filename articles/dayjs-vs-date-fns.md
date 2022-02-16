---
title: "日付ライブラリはdayjsかdate-fnsか"
emoji: "🤼"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [ライブラリ, 選定]
published: true
---

日付ライブラリについて dayjs を使うか date-fns を使うか比較[^1]してみました。
date-fns を使うことにしたので何を判断理由にしたのか書きます。
選び方に正解はないと思うので、ライブラリ選定についてよろしければ判断材料を教えてもらえたら幸いです 🙏

[^1]: 2022/02/16 時点のデータで比較しました

## 判断材料

### メンテナンス頻度

date-fns のほうがメンテナンスされています。
また、dayjs は 2021 年 12 月 17 日でコミットが止まっていますが、date-fns は 9 日前にコミットされています。
なので、date-fns のほうが活発に開発されているだろうと推測できます。
頻繁に開発されているので何かバグがあってもすぐ対応されることが期待できます。

- dayjs
  ![dayjsのコミットについて](https://gyazo.com/88f8e9b143a7685499a6e5e3a9a125f5.png=20x)
  ![dayjsのメンテナンス頻度](https://gyazo.com/4b16f9297388643b39209035b11f9d53.png=20x)

- date-fns
  ![date-fnsのコミットについて](https://gyazo.com/01984f7875edaf09cd04632e3384b6c8.png=20x)
  ![date-fnsのメンテナンス頻度](https://gyazo.com/73ad21c5888f5e479a75ddf99a7e333e.png=20x)

### 開発言語

dayjs は JavaScript のみで開発されているのに対して、
date-fns は TypeScript で開発している割合が多いです。
静的型付け言語はデファクトスダンダードになりつつあるので、
TypeScript で開発されているほうがよいと考えました。

![dayjsの開発言語](https://gyazo.com/6d9229fed8fae2dee6a761683f65dddf.png=20x)
_dayjs_

![date-fnsの開発言語](https://gyazo.com/4463207a4cb350cc790d2c6409976681.png=20x)
_date-fns_

### 周囲の意見

3~4 人にどの日付ライブラリを使っているか聞いたところ全員が date-fns を使っていました。
周囲に使っている人が多いと質問もしやすいのでいいですね。

### その他

他の比較要素として、GitHub のスター数や Contributor が何人くらいかなどが挙げられると思います。

## 公式

- dayjs
  [GitHub](https://github.com/iamkun/dayjs)
  [公式サイト](https://day.js.org/)
- date-fns
  [GitHub](https://github.com/date-fns/date-fns)
  [公式サイト](https://date-fns.org/)
