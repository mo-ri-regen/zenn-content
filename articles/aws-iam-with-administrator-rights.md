---
title: "管理者権限をもつIAMユーザを作成してみた"
emoji: "🤴🏼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, iam]
published: true
---

## この記事の目的

- IAM ユーザとは何かについて理解すること。
- 実際に IAM ユーザの作成ができること。  
   ※AWS マネジメントコンソールの画面はアップデートにより UI が変更される可能性があります。
  今回は IAM ユーザの作成まで行い、[次回](https://zenn.dev/mo_ri_regen/articles/aws-iam-user-mfa)は MFA の設定を行います。

## IAM とは

「AWS Identity and Access Management」の略であり、  
権限の設定をするために使われます。  
最初に AWS で作成したアカウントは root ユーザと呼ばれます。
root ユーザはすべてのリソースにアクセスでき、
なんでもできてしまうので、管理者権限をもつ IAM ユーザを
作成して適切な権限を設定します。
[AWS のベストプラクティス](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_root-user.html)にも、 root ユーザは最初の IAM ユーザ作成のときのみ使用し、そのあとは root ユーザではなく、IAM ユーザを使用するということが書かれています。

## IAM ユーザの作成

1. AWS マネージメントコンソールにログイン後、検索窓で「iam」と検索します。

   ![IAM検索](https://gyazo.com/5abdf88e5c41edc634e6a8c6c44ac683.png)

2. 「ユーザ」をクリック
   ![ユーザをクリック](https://gyazo.com/909240e16de1df08d81f91c8f6dc6cf6.png)

3. ユーザ名を入力し、「ユーザを追加」
   ![ユーザの追加](https://gyazo.com/76e6b024324202e9918edfe998f5f3f3.png)

4. 「アクセスの種類」の「AWS マネジメントコンソールへのアクセス」にチェックを入れます。  
   管理者権限の IAM ユーザは人が操作をするので、「プログラムによるアクセス」にチェックを入れる必要がありません。  
   「コンソールのパスワード」、「パスワードのリセットが必要」のチェックはデフォルトのままで構いません。
   ![アクセスの種類の設定](https://gyazo.com/ac52a5a383bbb9fa83462075e010fce3.png)

5. 「既存のポリシーを直接アタッチ」を選択し、「AdministratorAccess」を選択します。
   同じ権限を持つ場合は「アクセス権限を既存のユーザからコピー」を入力します。
   ![アクセス許可の設定](https://gyazo.com/4f8cf0a62b903806466543dffa8bbafe.png)

6. タグは、今回は追加しません。
   ![タグの追加](https://gyazo.com/05f377f9d26b373db232d17f987d1481.png)

7. 内容を確認し OK ならユーザの作成をクリックします。
   ![作成したアカウントの確認](https://gyazo.com/a7004b3ebc864f3535ae985deb3f07ed.png)

8. 「成功」と出ればユーザ作成が完了します。
   パスワードを表示させて、表示されたパスワードをメモします。(次回ログインのときに必要です)
   「E メールの送信」をクリックします。
   手順 4 で「パスワードのリセットが必要」にチェックを入れているため、
   パスワードの設定が必要になります。
   ![ユーザ作成完了](https://gyazo.com/ad35026c8da9498555bbc94106b766be.png)

9. メーラが立ち上がるので、サインイン URL に書かれた URL を開きます。
   ※URL を開くとサインインしていた AWS のコンソール画面から強制的にログアウトされてしまうので、**パスワードのメモ**を忘れないようにします。
   　パスワードを忘れた場合は パスワードを再作成する必要があります。  
   ![メーラ起動](https://gyazo.com/bd489d1bc85c726ff14eb7d143ecef4a.png)

10. 作成したアカウントでログインします。
    アカウント ID は root ユーザでログインしたときに確認可能です。  
    ![IAMユーザアカウントでログイン](https://gyazo.com/e8afb22075f1631bf009a9798de8d94e.png)

11. パスワードの変更を求められるので新しいパスワードを入力してログインします。
    ![パスワードの変更](https://gyazo.com/55731a3c90a6203eaf87f8980132d1b3.png)  
    これで、ユーザは作成できましたが、セキュリティを高めるために[次の記事](https://zenn.dev/mo_ri_regen/articles/aws-iam-user-mfa)で MFA の設定もしています。

## 参考 URL

- [IAM 公式ドキュメント](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/introduction.html)

- [AWS ベストプラクティス](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_root-user.html)
