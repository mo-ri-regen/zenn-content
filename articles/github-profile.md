---
title: "GitHubのプロフィールを設定してみよう!"
emoji: "😸"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [GitHub, プロフィール]
published: true
---

何もないGitHubのプロフィール画像ですが。。。
![GitHubのprofile画像(before)](https://gyazo.com/484634ab7a6019d0f5e35ef7708276c8.png)
こんな感じで、GitHubのプロフィールをもっと充実させる方法を紹介したいと思います😊
![GitHubのprofile画像(after)](https://gyazo.com/7b644097221ac22b3fb452fae7f5d1fb.png=50%)

## プロフィール編集方法

1. [GitHub公式サイト](https://github.com/)にアクセスしてみましょう。
2. 左側にあるNewをクリックして、新規リポジトリを作成
![新規リポジトリを作成](https://gyazo.com/5700380f53edace2677660223c4aa036.png)

3. リポジトリの設定をする。設定できたらcreate repositoryを押してリポジトリ作成する。
    :::message
    ※下記3点を設定してください。

    - リポジトリの名前をユーザ名(私の場合はmo-ri-regen)と同じにする。
    - publicにする。
    - Add a README fileにチェックを入れて、READMEを作成する。
    :::
    ![GitHubリポジトリ設定](https://gyazo.com/aa44b44e0e9fb46666347de86fad3ce2.png=100x)

4. 完成🎉

    ![GitHubプロフィールREADME](https://gyazo.com/413b8d3e48617ac1ceb31d53853a2f56.png)

    自分のプロフィール画面を見てみると反映されてます。
    ![GitHubプロフィール完成](https://gyazo.com/a4d713fb7813bd3ea9cbbbf1360a0bfc.png)

5. あとは、README.mdを好きなように編集すればOK

自由に書いてもOK(READMEにもコメントで書く内容について書かれてます)なのですが、有識者がGitHubに公開しているものを使うとほぼコピペでOKなので簡単です。
私はGitHubのコミット数などがわかる[GitHub Stats Card](https://github.com/anuraghazra/github-readme-stats)とpushされた使用言語の割合がわかる[Top Languages Card](https://github.com/anuraghazra/github-readme-stats#top-languages-card)の2つを設定しました。(mo-ri-regenのところは各自のユーザ名にしてください。)
オプションで[カラーテーマ](https://github.com/anuraghazra/github-readme-stats/blob/master/themes/README.md)や[レイアウト](https://github.com/anuraghazra/github-readme-stats#quick-tip-align-the-repo-cards)の変更ができます。

```
[![モーリー's GitHub stats](https://github-readme-stats.vercel.app/api?username=mo-ri-regen&theme=vue-dark&show_icons=true)](https://github.com/mo-ri-regen/github-readme-stats)

[![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=mo-ri-regen&theme=vue-dark&show_icons=true&layout=compact)](https://github.com/mo-ri-regen/github-readme-stats)
```

これで、設定完了です🥳
![プロフィール画像](https://gyazo.com/7b644097221ac22b3fb452fae7f5d1fb.png=100x)

参考のところに私のリポジトリのURLも載せておきます。

## 注意点

下記の場合はプロフィールに表示されません😲

:::message alert

- READMEに何も記載がないもしくはREADMEファイルがない
- リポジトリが**private**になっている。
- リポジトリが存在しない(リポジトリ名はユーザ名になってますか?)
:::

この中だと特に間違えやすそうなのが、
publicになっているかどうかだと思います😊
もし設定したのに表示されない場合は上記3点を確認してみましょう

## 参考

- [プロフィール編集方法(GitHub公式)](https://docs.github.com/en/github/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme)
- [Top Languages Card](https://github.com/anuraghazra/github-readme-stats#top-languages-card)
- [カラーテーマ変更](https://github.com/anuraghazra/github-readme-stats/blob/master/themes/README.md)
- [ブログ参考記事](https://blog.ko31.com/202007/how-to-create-the-github-profile-readme/)
- [Qiita参考記事](https://qiita.com/zizi4n5/items/f8076cb25bbf64a9bc1c)
- [私のGitHubリポジトリ](https://github.com/mo-ri-regen)