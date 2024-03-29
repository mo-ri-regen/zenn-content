---
title: "正規表現のシンタックスシュガーを学ぶ"
emoji: "🍩"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [正規表現]
published: true
---

前回、正規表現の基本演算を[紹介した](https://zenn.dev/mo_ri_regen/articles/regular-expression-3basic-operations)ので気になる方はそちらもお読みください 👋

基本演算だけだと冗長になりますが、シンタックスシュガーを使うことで簡単に書くことができます。

## プラス演算(+)

$+$は 1 回以上の任意の繰り返しを表します。

-  例
  ab+c は abbbbc といった少なくとも b が 1 文字以上含んだ文字列を表現できます。

$r$ という正規表現に対して $r+$は $r(r)*$ と書き換えることができます。

## 疑問符演算(?)

$?$をパターンの後ろにつけることで、パターンの 0 回か 1 回の繰り返しを表します。
つまり、?がつくとその文字は現れるか現れないかどちらかということを表しています。

- 例
  https?://zenn.dev/ は http://zenn.dev/ と https://zenn.dev/ どちらも表します。

## 範囲量指定子($\{n,m\}$)

$n \le m$ のとき$\{n,m\}$は最少 $n$ 回から最多 $m$ 回までの繰り返しを表します。
$n=m$のときは$\{n\}$と一つだけ書くことができます。$\{n,\}$と書くと$n$回以上の繰り返しを表します。

- 例
  x{1,3}は x|xx|xxx と同値です。

## ドット(.)

任意の 1 文字を「.」で表します。

- 例
  「r.\*e」という正規表現には「rare」といった r から始まって e で終わる任意の文字列がマッチします。
  :::message
  「.」は"任意"の 1 文字を表すのでスペースや記号など何でも OK です。
  上記の正規表現では、「r ae」、「r@example」、「r4e」などもマッチします。
  :::

## 文字クラス

\[\](ブラケット)に表現したい文字を詰め込みます。 ハイフン(-)で範囲指定できます。ASCII の文字コードの順番になっているので、[A-z]だと^や\_などの 6 つの記号が含まれます。

- 例
  [0-9]は 0〜9 までの数字を表します。
  [a-z]は小文字のみのアルファベットを表します。
  [A-Z]は大文字のみのアルファベットを表します。
  [a-zA-Z]は大文字、小文字を含むアルファベットを表します。

[0-9]は[0123456789]と書くことができ、ブラケットを使わないと 0|1|2|3|4|5|6|7|8|9 となります。「-」も  文字クラスでマッチする文字列に含めたい場合は「-a-z」や「a-z-」などブラケット内の先頭かブラケット内の末尾に「-」を含めることで表現できます。

### 否定(^)

 ブラケットの内部で先頭の^(ハット)は否定の記号として扱われます。

- 例
  [\^0-9a-zA-Z]は数字やアルファベット以外の文字列を表します。

## エスケープシーケンス

「\」を用いることで改行やタブなどを表現できます。

- 例
  改行は「\n」、タブ文字は「\t」
  特殊な例として[0-9]には\d,[0-9a-zA-Z]には\w が多くの処理系で割り当てられています。

### メタ文字のエスケープ

演算子を普通の文字として認識させるためにエスケープシーケンスを使うことができます。

- 例
  「a\*b」という文字列にマッチさせたい場合、「a\\\*b」と表現します。

## アンカー

位置にマッチするメタ文字です。特定のシンボルやエスケープシーケンスを用います。

| アンカー | 位置           |
| -------- | -------------- |
| ^        | 行頭           |
| $        | 行末           |
| \A       | テキスト先頭   |
| \b       | 文字列の間     |
| \B       | 文字列の間以外 |
| \z       | テキスト終端   |

- 例
  aaa bbb に対して「(a+ )\\b(b+)」の「(a+ )」は前半の「aaa 」にマッチし、「(b+)」は後半の「bbb」にマッチします。そして、「\\b」は文字列の間という位置にマッチしています。

## 参考

[正規表現技術入門――最新エンジン実装と理論的背景](https://gihyo.jp/book/2015/978-4-7741-7270-5)
