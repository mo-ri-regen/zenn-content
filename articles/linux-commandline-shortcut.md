---
title: "Linuxでコマンドラインを編集するのに知っておくべきショートカット集"
emoji: "◼️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Linux, bash]
published: true
---

## 目的

Linuxでコマンドラインを編集するのに知っておくと便利なショートカットである「カーソル移動」、「文字の削除」、「ヤンク」、「画面をクリアにする方法」についてそれぞれ書いてます。

## シェルの移動方法

カーソル(←,↓,↑,→)を使っても移動できますが、コマンドを覚えることでホームポジションを崩さずに移動することができます。

### 1文字前に移動
- コマンド
Ctrl + b[^1]
- 例
移動前
![移動前](https://gyazo.com/c8445b41e3acfc53b54578f15a6d2f1c.png)
移動後
![1文字前に移動](https://gyazo.com/bdf9d6a94046e9293f41b4ceb5221970.png)
### 1文字後ろに移動
- コマンド
Ctrl + f[^2]
- 例
移動前
![移動前](https://gyazo.com/c8445b41e3acfc53b54578f15a6d2f1c.png)
移動後
![1文字後ろに移動](https://gyazo.com/e217cc3fbc9d20eb0a73b5c2ea9d556d.png)

[^1]:backの"b"
[^2]:forwardの"f"

### 行頭に移動
- コマンド
Ctrl + a
- 例
移動前
![移動前](https://gyazo.com/c8445b41e3acfc53b54578f15a6d2f1c.png)
移動後
![行頭に移動](https://gyazo.com/20ca0dcb826d31eb04faca7e4ca8793e.png)
### 行末に移動
- コマンド
Ctrl + e
- 例
移動前
![移動前](https://gyazo.com/c8445b41e3acfc53b54578f15a6d2f1c.png)
移動後
![行末に移動](https://gyazo.com/d7ac71860c7558ae86f5aca91b714b50.png)

## 削除

### カーソル位置の後方に1文字削除

- コマンド
「Ctrl + h」またはBackSpace

- 例
削除前
![Ctrl + hで削除前](https://gyazo.com/b65523b5e8967251f0eb243fb3c8376e.png)
削除後
![Ctrl + hで削除後](https://gyazo.com/a9fef154e5c1d32457c66abc4d2f60e7.png)

### カーソル位置の1文字削除
- コマンド
「Ctrl + D」またはDelete

- 例
削除前
![Ctrl + Dで削除前](https://gyazo.com/b65523b5e8967251f0eb243fb3c8376e.png)
削除後
![Ctrl + Dで削除後](https://gyazo.com/19b9e990af9513f08f826da0f735ff70.png)

### 後方にスペース区切りで1単語分を削除

- コマンド
Ctrl + w

- 例
削除前
![1単語分削除前](https://gyazo.com/fbe47742e8a751b08002f5ec32b193cc.png)
削除後
![1単語分削除後](https://gyazo.com/b17afd193284977bca508006e16c14d2.png)

## カット

操作するときは単純に削除するのではなく、カーソル位置から行頭までする→ヤンク(ペースト)するというようにいわゆるコピペ作業するときに使います。

### カーソル位置から行末まで削除

- コマンド
Ctrl + k

- 例
削除前
![Ctrl + kで削除前](https://gyazo.com/c62003497e8f211c984a2b65562ab039.png)
削除後
![Ctrl + kで削除後](https://gyazo.com/90f793336605ccafd2dee9b3e645190e.png)

### カーソル位置から行頭までを削除
- コマンド
Ctrl + u

- 例
削除前
![Ctrl + uで削除前](https://gyazo.com/c62003497e8f211c984a2b65562ab039.png)
削除後
![Ctrl + uで削除後](https://gyazo.com/042b629231305048998f662c40984702.png)


## ヤンク

bashではペーストのことを**ヤンク**といいます。
### 最後に削除した内容を挿入
- コマンド
Ctrl+y
- 例
Enter押す前にCtrl + uで削除します。
![Ctrl+uで削除前](https://gyazo.com/735cd9c7af431e2c85fd5d49e7020861.png)
削除されました。
![Ctrl+uで削除後](https://gyazo.com/388ca5f88d81e86d3fcacce4d7481607.png)
Ctrl+yを押すとヤンクされます。
![Ctrl+yでヤンク](https://gyazo.com/ee4ec477dc77eb3c8ec4b20f4405b534.png)

## 画面クリア

下記コマンドで画面に表示している内容をクリアします。
```bash
clear
```

## 参考

https://www.sbcr.jp/product/4797380941/
