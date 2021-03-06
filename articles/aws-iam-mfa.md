---
title: "IAMユーザのMFAの設定"
emoji: "🤴🏼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, iam]
published: true
---

## この記事の目的

[前回](https://zenn.dev/mo_ri_regen/articles/aws-iam-with-administrator-rights)作成した IAM ユーザのセキュリティを高めるために MFA の設定をする。

## MFA とは

「Multi-Factor Authentication:多要素認証」の頭文字を取って MFA と呼ぶ。  
DB に登録したパスワード+ワンタイムパスワードなど複数のパスワードを入力させることで
セキュリティを高める。

## MFA の設定

1. Chrome の拡張機能である[Authenticator](https://chrome.google.com/webstore/detail/authenticator/bhghoamapcdpbohphigoooaddinpkbai?hl=ja)を追加する。

2. AWS マネジメントコンソール画面に行き、IAM で追加したユーザを選択する。  
   ![ユーザ選択](https://gyazo.com/a3ee033758d0a4032c63f3e217dbc5d5.png)

3. 「認証情報」タブの「MFA デバイスの割当」の「管理」をクリック。
   ![MFA デバイスの割当](https://gyazo.com/51d84f8a3f6f2d98d8f34d55578910a7.png)

4. 「仮想 MFA デバイス」のラジオボタンにチェックが入っていることを確認する。
   ![仮想MFAデバイスの選択](https://gyazo.com/663f4e9629536a27846631a813ad0c2a.png)

5. QR コードの表示のところをクリックする。  
   ![QRコード表示](https://gyazo.com/f841f06ded2be43163573c675b641a79.png)
6. 右上の鉛筆マークをクリックして、「+」をクリックする。  
   ![鉛筆マークをクリック](https://gyazo.com/55233ac756fd2b186f307315a5c90560.png)

   !["+をクリック"](https://gyazo.com/7437fbbe7d5b6fdd466e13c4674865a3.png)

7. 手順 5 で表示された QR コードをスキャンするとユーザが追加できる。  
   ![QRコードのスキャン](https://gyazo.com/5ec813b0fd5cb2541d26f4b723ccd8c7.png)

   ![ユーザの追加](https://gyazo.com/8bda5d9a78dc6d2eb915a4c27ea4a951.png)

8. 1 で追加した「Authenticator」を起動すると**登録したユーザ**(今回の例では test-admin1)の認証コードが**2 回**出てくるので、MFA コードをそれぞれ記入する。(画像では複数ユーザ登録しているが、初めて登録した場合は 1 人分しか表示されないので注意する。)
   時間切れになった場合は再度、「Authenticator」を実行すれば別のコードが記入される。

![MFAコードの表示](https://gyazo.com/cb31b0edb16f0a797fd0fa2502900ec2.png)

※サンプルでは時間が間に合わなかったため、入力した数字は異なっているが、
本来は表示された MFA コードを入力する。

![MFAコードの記入](https://gyazo.com/5efa166f0924acefb54f03b1d1d377cc.png)

下記画像が出れば、MFA コードの割当は成功です 🎉
お疲れさまでした 😊
![MFAコード割当成功](https://gyazo.com/8c8c89e3a532eff1787e695abe9fe413.png)

## 最後に

ボタンを押すだけで簡単に設定できました。
aws にも CLI 使って操作できるようなので、操作に慣れていったら勉強したいなと思います。  
ユーザを作成しただけなので、今後は、各アクセス権限についての意味について調査したいと思ってます。

## 参考 URL

- [MFA について(公式)](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_credentials_mfa.html)
- [MFA](https://e-words.jp/w/%E5%A4%9A%E8%A6%81%E7%B4%A0%E8%AA%8D%E8%A8%BC.html)
