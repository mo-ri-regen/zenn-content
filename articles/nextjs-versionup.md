---
title: "Nextjsのバージョンアップのやりかた"
emoji: "🎉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [nextjs, npm, yarn]
published: true
---

先日、nextjs11 のバージョンアップ情報が発表されました 🎉
今回はバージョンを上げる方法についてみていきます 👀

## バージョンアップの方法

package.json でインストールされている nextjs のバージョン確認
![バージョン確認](https://gyazo.com/19aa1d88f81927ac00446a73197d9227.png)

下記コマンドを打ちます。

```bash
# npm
npm i next@latest react@latest react-dom@latest

# yarn
yarn add next@latest react@latest react-dom@latest
```

package.json をみて、最新版か確認します。
無事、バージョン 11 へアップデートできました。
![バージョンアップ](https://gyazo.com/af89adb33c9bc6de65c49722099e6917.png)

ver11 は ESLint がデフォルトでサポートされていたり、Image タグの幅と高さが指定しなくてもそれぞれ自動で定義されたりとますます便利になりましたね。

## 参考

[バージョンアップ内容](https://nextjs.org/blog/next-11?utm_source=next-site&utm_medium=button&utm_campaign=next-conf)
