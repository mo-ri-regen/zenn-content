---
title: "ファイル名にスペースがあるときのGitコマンドの使い方"
emoji: "📁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [git]
published: true
---

## エラー内容

下記のようにファイル名にスペースがあると、コマンドだと認識されてしまうためエラーとなります。

```bash
git add file name
fatal: pathspec 'file' did not match any files
```

## 解決策

パスを""で囲むとスペースがあってもエラーを出さずに commit できます。

```bash
git add "filename"
```

:::message
予期せぬエラーが起きうるため、ファイル名にスペースを入れないほうがよいでしょう。
ファイル名を区切りたいときは、スネークケースにするかキャメルケースにしたほうがよいと思います。
:::
