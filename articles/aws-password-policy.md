---
title: "AWSのパスワードポリシー設定方法"
emoji: "👮‍♂️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, iam, セキュリティ]
published: true
---

コンソールにログインするためのカスタムパスワードポリシーの設定を行おうと思います。
IAMからカスタムパスワードポリシーの設定ができます。

ちなみにデフォルトでは下記のようなパスワードポリシーになっています。

> パスワードの文字数制限: 8～128 文字
> 大文字、小文字、数字、! @ # $ % ^ & * ( ) _ + - = [ ] { } | ' 記号のうち、最低 3 つの文字タイプの組み合わせ
> AWS アカウント名または E メールアドレスと同じでないこと

## コンソールで設定

1. [コンソール](https://console.aws.amazon.com/iam/)にサインインして、左ペインのダッシュボードにアカウント設定があるのでそれをクリックします。

   ![アカウント設定をクリック](https://gyazo.com/297afde3165f74acd3bcc4bf5384d4e5.png =130x)

2. 「パスワードポリシーを変更する」ボタンをクリックします。

   ![「パスワードポリシーを変更する」ボタンをクリック](https://gyazo.com/0a5af55a6219c587a9b7cee0247ba5a7.png)

3. 内容を読んで設定すれば完了 🎉

   ![パスワードポリシーの設定](https://gyazo.com/e6da9f2835b5fbfc4ad1fc1fd63ffa78.png)

## CLI で設定

CLI は[こちら](https://aws.amazon.com/jp/cli/)からダウンロードできます。
下記コマンドでパスワード設定できるようです。(動作未確認)

```bash
# カスタムパスワードポリシーの作成またはカスタムパスワードポリシーの変更
aws iam update-account-password-policy
# パスワードポリシーの表示
aws iam get-account-password-policy
# カスタムパスワードポリシーの削除
aws iam delete-account-password-policy
```

## 参考

https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html
