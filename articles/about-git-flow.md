---
title: "チーム開発で使われるGitFlowについて"
emoji: "👨‍👩‍👦‍👦"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Git]
published: true
---

## この記事の目的

Git Flow について理解する

## GitFlow とは

Git をチームで使う上での運用方法を表したものです。
GitFlow は複雑なので、実際に運用するときは[GitHubFlow](https://guides.github.com/introduction/flow/)などシンプルなフローを使われることが多いです。

![GitFlow](https://storage.googleapis.com/zenn-user-upload/dc17ae3e6fed6e7168b69513.png =400x)_全体図_

:::message
現在は master ではなく main という名前に変えようという動きがあるので、この記事でも main と表記します。
図では master と書いていますが main ブランチのことだと読みかえてください。
:::

## main ブランチ

このブランチで開発は行いません。main ブランチの最新版がプロダクトとしてユーザにリリースされます。

## develop ブランチ

main から develop へブランチを切ります。develop で開発を行い、main はリリース時にコミットされます。main の commit にはリリースごとにタグを打ちます。

![developブランチ](https://storage.googleapis.com/zenn-user-upload/5337cf163444e159e35792e6.png =150x)

## feature ブランチ

develop から feature へブランチを切ります。
複数人で develop で開発するときに使います。1 機能ごとに develop からブランチを切り、1 機能の開発が終われば develop へ merge します。
大きい機能の場合は feature からさらに feature へブランチを切ります。
最終的に製品に入れるかどうかわからないときも feature ブランチを使います。

![featureブランチ](https://storage.googleapis.com/zenn-user-upload/5337cf163444e159e35792e6.png =150x)

## release ブランチ

develop から main へ merge するための準備をするブランチです。main へ commit することで実際にプロダクトとして使われるようになります。
"準備"とある通り release で新規機能は追加してはいけません。

### 準備の例

- bugfix のみに使う
- version 表記やタイムスタンプを更新する
- Apple や Google の審査に使う

## hotfix ブランチ

main から hotfix へブランチを切ります。本番環境で発生したバグのうち緊急性の高いものを修正するブランチです。
修正が完了したら main と develop(or release)にマージします。
main へマージしたらパッチバージョンを上げることが多いです。
(ex. 1.2.0→1.2.1 へ上げる)

![hotfixブランチ](https://storage.googleapis.com/zenn-user-upload/30087270190162f1ae6a4f3b.png =300x)

## 参考

https://www.youtube.com/watch?v=aZ90usArA6g

https://nvie.com/posts/a-successful-git-branching-model/
