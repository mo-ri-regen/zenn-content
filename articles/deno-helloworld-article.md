---
title: "denoでHelloプログラム書いてみた"
emoji: "🦕"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [deno]
published: true
---

## denoとは

node.jsを作った人がnode.jsの悪かったところを改善したものです。
たとえば、デフォルトでTypeScriptに対応しており、パッケージを管理するのにnode_modulesを使いません。

## インストール方法

Homebrewを使えば簡単にdenoをインストールできます。

```bash
brew install deno
```

Windowsのかたやその他の方法でインストールするかたは[こちら](https://deno.land/manual@v1.12.0/getting_started/installation)を参考にしてください。

## 動作確認

サンプルを動かしてみましょう

```ts:hello-world.ts

 function capitalize(word: string): string {
    return word.charAt(0).toUpperCase() + word.slice(1);
  }
  
  function hello(name: string): string {
    return "Hello " + capitalize(name);
  }
  
  console.log(hello("john"));
  console.log(hello("Sarah"));
  console.log(hello("kai"));

```

実行するにはターミナルで下記コマンドを打ちます。

```bash
deno run hello-world.ts
```

下記、実行結果が出れば成功です。

```bash
Hello John
Hello Sarah
Hello Kai
```

## 感想

まだ、サンプルをコピペしただけなので何ができて何ができないのかもう少し触ってみたいですね。

## 参考

https://deno.land/
