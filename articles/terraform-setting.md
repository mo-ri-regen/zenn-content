---
title: "Terraformのインストールから設定まで"
emoji: "👩‍💻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [terraform, iac, 初心者]
published: true
---

## 前提条件

macOS Sequoia Version 15.1.1 (24B91)
Homebrew 4.4.13

:::message
MacBook に Homebrew がインストールされていればインストールできると思います
Windows のインストール手順は公式サイト[^1]を参照してください
:::

## インストール手順

1. HashiCorp の公式リポジトリを Homebrew に追加する

```bash
brew tap hashicorp/tap
```

2. hashicorp/tap リポジトリから Terraform をインストールする

```bash
brew install hashicorp/tap/terraform
```

3. インストールできているか確認

バージョンが表示されていればインストール完了です

```bash
terraform --version

Terraform v1.10.3
on darwin_amd64
```

## 拡張機能

Terraform を使いやすくするために拡張機能をインストールしましょう
オススメの拡張機能は検索型の生成 AI エンジン[felo](https://felo.ai/ja/search)に聞きました

https://felo.ai/search/6u8gzopoXJHymPHP6FB8jc?invite=JPynwGEBODBdr

### [HashiCorp Terraform](https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform)

ハイライトや VS Code のフォーマットをしてくれます

https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform

### [Infracost](https://marketplace.visualstudio.com/items?itemName=Infracost.infracost)

Terraform で書いたコードを実行したときに発生するコストを見積もるツールです

[![Infracostのデモ画面](https://i.gyazo.com/ffa9d980770f5725b78c204c09f8c09a.png)](https://gyazo.com/ffa9d980770f5725b78c204c09f8c09a)

https://marketplace.visualstudio.com/items?itemName=Infracost.infracost

### [Terraform Advanced Syntax Highlighting](https://marketplace.visualstudio.com/items?itemName=pjmiravalle.terraform-advanced-syntax-highlighting)

構文ハイライトを大幅に改善してくれるツールです

https://marketplace.visualstudio.com/items?itemName=pjmiravalle.terraform-advanced-syntax-highlighting

## 認証情報の設定

だれでもアクセスできると問題があるので AWS など使いたいクラウドサービスの認証情報を Terraform に設定する必要があります
AWS ではアクセスキーとシークレットアクセスキーを発行して設定できます[^2]

最初に.bashrc や.zshrc に直接、環境変数を設定すると起動するたびに環境変数を設定しなくてよいので便利です

### 手順

1. 使っているシェルの確認

```bash
echo $SHELL
/bin/zsh
```

ローカルでは zsh を使っていることがわかりました

2. 環境変数の設定

vim を使って直接、書き込んでも問題ありません
今回はコマンドを実行して書き込んでいきます
環境変数名は 1 文字でも違うと認識されなくなるのでコピペしましょう

```bash
echo 'export AWS_ACCESS_KEY_ID="YOUR_ACCESS_KEY"' >> ~/.zshrc
echo 'export AWS_SECRET_ACCESS_KEY="YOUR_SECRET_KEY"' >> ~/.zshrc
```

:::message
書き込む場所はお使いのシェルに合わせて変更してください
:::

## 参考

https://developer.hashicorp.com/terraform/install

https://qiita.com/Hikosaburou/items/1d3765d85d5398e3763f

[^1]: 「参考」に公式サイトのリンクを記載しています。
[^2]: アクセスキー、シークレットアクセスキーの生成方法は省略します。時間があれば、執筆するかも...
