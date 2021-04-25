---
title: "Gitの概念"
emoji: "🤔"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Git]
published: false
---

## 目的

Git とは何か、何が便利なのかについて記載する。

## 説明しないこと

- Git コマンド
- GUI ツール
- ブランチやコンフリクトなどの細かい用語説明
- コンフリクトの解消方法など実践的な内容

## Git とは

Linux を開発した Linus Torvalds(リーナス・トーバルズ)が開発。  
分散型のバージョン管理システムでスナップショットで記録している。
誰が、いつ、なんの変更を行ったか追いかけることが可能。
分散型にすることで、複数人で開発するときに他の人の変更を気にすることなく開発ができ、
スナップショットで記録することでブランチ操作やマージ操作がそれぞれしやすくなる。
(以前は [svn](https://subversion.apache.org/) など集中型のバージョン管理システムが使われていた。)

## Git が使われなかった場合のバージョン管理方法

- よくあるファイル管理方法

1. file_20210401.md
2. file_20210402.md
3. file_20210403.md

### 問題点

- 更新されるたびにファイルが増えていく
- ファイル名を変更していくので、更新に手間がかかる
- 上記の例の場合、同じ日にファイルの更新履歴を作成することが不可能
- 複数人で作業している場合、コンフリクト(衝突)の解決が困難

### Git による解決方法

Git はコミットと呼ばれる最新の記録からたどっていくことで、誰がいつどんな変更を行ったかを
把握することができるためファイル名を変えなくてもよい。
後述のホスティングサービスを使うことで複数人での開発がやりやすくなった。
Git コマンドを覚えないといけないが、SourceTree や VSCode など GUI 上で操作できるツールも増えてきた。

## Git の作業手順

ワークツリー、ステージ、リポジトリの 3 つのエリアがそれぞれある。
ユーザがワークツリー(ローカルで作業した内容)をステージ(コミットする変更を準備する場所)へ add(追加)し、add したあとローカルリポジトリへコミット(スナップショットを記録)する。
コミットしたらローカルリポジトリからリモートリポジトリ(GitHub などのホスティングサービス)にプッシュする。

![gitの作業図](https://storage.googleapis.com/zenn-user-upload/bxukitxw6mvqfb78ro36hytxhzov)

## Git のホスティングサービス

Web 上でソースコードを管理するサービス。
複数人でコード開発するために便利な機能がある。
流れとしては、(詳しくは解説しないが事前に GitHub Flow を用いてブランチを切ることが多い)開発者がプルリクエストを投げると、
責任者がコードレビューを行いよければそのままメインブランチにマージし、
改善点があれば指摘する。改善点がある場合は、指摘された部分を直した後に
ホスティングサービスに push し、またコードレビューを行ってもらう。
改善されるまでこの流れを続ける。
以下、ホスティングサービスを一部紹介する。

### [GitHub](https://github.com/)

GitHub 社が運営していたが[Microsoft(MS) に買収された](https://news.microsoft.com/announcement/microsoft-acquires-github/)。  
プライベートリポジトリは以前は有料だったが、無料になるなどユーザにとって使いやすくなってきている。
OSS の開発では GitHub が主流となっており、ホスティングサービスとしてはデファクトスタンダードとなっている。[Google トレンド](https://trends.google.com/trends/explore?date=today%205-y&q=bitbucket,gitlab,%2Fm%2F0ryppmg)を見ても GitHub でググっている人は圧倒的に多い。
[料金](https://github.com/pricing)はリンク先参照。

### [GitLab](https://about.gitlab.com/)

MIT ライセンス。Gitlab 社が運営。ロゴはキツネではなく、[たぬき](https://www.publickey1.jp/blog/20/gitlab.html)のようです。
非公式だが、日本語の[コミュニティサイト](https://www.gitlab.jp)もある。
GitHub が MS にされたときに GitLab へ移行したユーザもいる模様。
GitHub を除外して[Google トレンドで比較](https://trends.google.com/trends/explore?date=today%205-y&q=bitbucket,gitlab)すると 2021 年 4 月時点では GitLab のほうが BitBucket の 2 倍近くググられている。
[料金](https://www.gitlab.jp/pricing/)はリンク先参照。

### [BitBucket](https://bitbucket.org/)

Atlassian が運営。使ったことがないので詳しくはわかりません 🙇‍♀️
プライベートリポジトリが無料。人数制限(5 人まで)があるため、スモールチームで開発する人向け。
[料金](https://www.atlassian.com/software/bitbucket/pricing)はリンク先参照。

## 注意点

GitHub 上で公開していた[三井住友の業務システムのソースコードが一部流出](https://xtech.nikkei.com/atcl/nxt/news/18/09551/)していたニュースが話題になりました。
GitHub は public で公開すると誰でもみれてしまうため機密情報をアップしないようにしましょう。
一例として、[AWS で取り扱う秘密鍵を公開](https://dev.classmethod.jp/articles/accesskey-leak/)してしまって、不正な操作が行われたり莫大な請求がきてしまったりすることもあるようです。

## 余談(ブランチ名について)

2020 年 6 月から GitHub で新規作成したブランチが デフォルトで[master から main に変更](https://github.com/github/renaming)になりました。
理由としては master という単語が「主人」という意味を持ち、海外では奴隷制度を連想されるため
main に変更になりました。
なので、昔の記事を読むとブランチ名が master となっていることがありますが、
main ブランチだと読み替えてもらえばと思います。
また、そのような流れがあることから main という名前を使っていきましょう 😊

## 参考

### Udemy

- [Git：もう怖くない Git！チーム開発で必要な Git を完全マスター ](https://www.udemy.com/course/unscared_git/)([山浦 清透](https://twitter.com/kiyotoyamaura))
- [米国 AI 開発者がやさしく教える Git 入門講座](https://www.udemy.com/course/aigitgithub/)([かめ れおん](https://twitter.com/usdatascientist))

### 書籍

リック・ウマリ(2016)『[独習 Git](https://www.seshop.com/product/detail/18861)』,吉川邦夫（訳）,翔泳社

### URL

- [main ブランチについて(公式)](https://github.com/github/renaming)
- [main ブランチについての記事(日本語版)](https://www.infoq.com/jp/news/2020/11/github-main-branch/)
- [GitLab のロゴについて](https://www.publickey1.jp/blog/20/gitlab.html)
