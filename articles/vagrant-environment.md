---
title: "Vagrantを使った環境構築"
emoji: "🚀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [vagrant, 環境構築]
published: true
---

## 準備

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)
- package.box[^1](Vagrantfile から作成)

[^1]: box 名はオプションで任意の名前に変更できます。ファイルサイズが数 GB あるのでダウンロードには時間がかかります。

## 環境構築方法

package.box をローカルの任意の場所に保存します。

:::message
package.box は下記コマンドで Vagrantfile から作成できます。

```bash
vagrant package
```

チームで共有するときは他の人から box ファイルを作成してもらう必要があります。

:::

### box 追加

```bash
vagrant box add any_box_name
```

下記コマンドで追加されたボックスを確認できます。

```bash
vagrant box list
```

### vagrantfile 作成

```bash
# packageはboxの名前
vagrant init package
```

### 起動

vagrantfile が生成されたら up コマンドで起動します。

```bash
vagrant up
```

### 停止

停止するときは

```bash
vagrant halt
```

で停止します。

### 再起動

vagranfile を編集したら reload をします。

```bash
vagrant reload
```

成功したら下記のようなメッセージが出ます。

```bash
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: hostonly
==> default: Forwarding ports...
    default: 22 (guest) => 1234 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:1234
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Setting hostname...
==> default: Configuring and enabling network interfaces...
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
```

## 参考

[GitHub](https://github.com/hashicorp/vagrant)
[公式サイト](https://www.vagrantup.com/)
