---
title: "VagrantからVirtualBoxを起動できない"
emoji: "😖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [vagrant, virtualbox, エラー]
published: true
---

業務で Vagrant を使うときにエラーでハマったことを書きます。

## 環境

virtualbox 6.1.26
Vagrant 2.2.18
Windows10 Pro

## エラー内容

Vagrant から VirtualBox を起動するために

```bash
vagarant up
```

を行うと下記エラーが出ました。

```bash
Stderr: 0%...
VBoxManage.exe: error: Failed to create the host-only adapter
VBoxManage.exe: error: Querying NetCfgInstanceId failed (0x00000002)
VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component
HostNetworkInterfaceWrap, interface IHostNetworkInterface
```

どうやらホストオンリーアダプターの作成に失敗しているようでした。
ホストオンリーアダプターとは[ホスト OS とゲスト OS のみが通信できるネットワーク](https://vboxmania.net/%e3%83%8d%e3%83%83%e3%83%88%e3%83%af%e3%83%bc%e3%82%af%e8%a8%ad%e5%ae%9a/)のことで設定されないとホストマシンから仮想マシンへの通信ができないようです。

## 解決策

### 結論

Vagrant から VirtualBox を起動する間のときだけウイルス対策ソフトをオフにする

### プロセス

vagrantfile で下記のように IP アドレスを設定している箇所でエラーが起きていることがわかりました。

```
config.vm.network "private_network", ip: "192.168.33.10"
```

いろいろ調べていると、[Qiita の記事](https://qiita.com/iscale821/items/9f561ba4b34ce1b7700c)で

> プロンプトで virtualbox のファイルが置いてあるフォルダに行って
> VBoxManage.exe hostonlyif create
> と入力するとホストオンリーアダプターを作成することができました。その際にウィルスバスターを一時的に無効にする必要がありました。
> 結局インストールするときにウィルスバスターが邪魔してアダプターの作成がうまく行われなかったのかな？

と書かれているのを発見しました。
ウイルス対策ソフトをオフにしたあと、VBoxManage.exe(私の環境では C:\Program Files\Oracle\VirtualBox にありました)を下記の通り実行。

```bash
VBoxManage.exe hostonlyif create
```

するとホストオンリーアダプターが作成されました。
その後に

```bash
vagrant up
```

を実行すると無事、VirtualBox が起動できました 🎉
VirtualBox が起動できたらウイルス対策ソフトはオンに戻しましょう。

## 余談

[stackoverflow](https://stackoverflow.com/questions/69864455/virtualbox-6-1-28-fails-to-load-r0-module-verr-ldr-general-failure-on-window)によると virtualbox6.1.28 にはバグがあるようです。(6.1.30 でもまだ直っていないようです。)

## 参考

[VirtualBox のネットワーク設定](https://vboxmania.net/%e3%83%8d%e3%83%83%e3%83%88%e3%83%af%e3%83%bc%e3%82%af%e8%a8%ad%e5%ae%9a/)
[Virtual Box のホストオンリーネットワークが設定できない...](https://qiita.com/iscale821/items/9f561ba4b34ce1b7700c)
