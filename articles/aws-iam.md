---
title: "管理者権限をもつIAMユーザを作成してみた"
emoji: "🤴🏼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, iam]
published: false
---

## この記事の目的

- IAM ユーザとは何かについて理解すること
- 実際に IAM ユーザ作成までの手順について記すこと。  
  ※AWS マネジメントコンソールの画面はアップデートにより UI が変更される可能性があるのでご了承ください。

## IAM とは

「AWS Identity and Access Management」の略であり、  
権限の設定をするために使われる。  
最初に AWS で作成したアカウントは root ユーザと呼ばれる。
root ユーザはすべてのリソースにアクセスでき、
なんでもできてしまうので、管理者権限をもつ IAM ユーザを
作成して適切な権限を設定する。
[AWS のベストプラクティス](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_root-user.html)にも、 root ユーザは最初の IAM ユーザの作成のときのみ使用し、そのあとは root ユーザではなく、IAM ユーザを作成するということが書かれています。

## IAM ユーザの作成

1. AWS マネージメントコンソールにログイン後、検索窓で「iam」と検索する。

![IAM検索](https://gyazo.com/5abdf88e5c41edc634e6a8c6c44ac683.png)

2. 「ユーザ」をクリック
   ![ユーザをクリック](https://gyazo.com/2f2066a3aa1a307bd1bc0427d2f57216.png)

3. ユーザ名を入力し、「ユーザを追加」
   ![ユーザの追加](https://gyazo.com/76e6b024324202e9918edfe998f5f3f3.png)

4. 「アクセスの種類」の「AWS マネジメントコンソールへのアクセス」にチェックを入れる。  
   (管理者権限の IAM ユーザは人が操作をするので、「プログラムによるアクセス」にチェックを入れる必要がない)  
   「コンソールのパスワード」、「パスワードのリセットが必要」のチェックはデフォルトのままでよい
   ![アクセスの種類の設定](https://gyazo.com/ac52a5a383bbb9fa83462075e010fce3.png)

5. 「既存のポリシーを直接アタッチ」を選択し、「AdministratorAccess」を選択する。同じ権限を持つ場合は「アクセス権限を既存のユーザからコピー」を入力する。
   ![アクセス許可の設定](https://gyazo.com/4f8cf0a62b903806466543dffa8bbafe.png)

6. タグの追加
   ![タグの追加](https://gyazo.com/05f377f9d26b373db232d17f987d1481.png)

## IAM ポリシーの適用 → 実際に権限のことしかできないのか確かめる

## 最後に

ボタンを押すだけで簡単に設定できました。
今後は、各アクセス権限についての意味について調査したいと思ってます。

## 参考 URL

- [IAM 公式ドキュメント](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/introduction.html)
