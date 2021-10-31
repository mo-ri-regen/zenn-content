---
title: "dockerignoreの書き方"
emoji: "🙈"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Docker, Dockerfile]
published: true
---

.dockerignore に記載のあるファイルはコンテキスト(docker イメージ構築に必要な素材・内容物)から除外されます。

## ルール

"#"で始まる行はコメントとみなされます。
除外したいファイルやディレクトリの名前を書きます。

```Docker
# この行はコメント

# root以下のあらゆるサブディレクトリ内でtempで始まる名前やファイルの除外
# ex. /somedir/temporary.txt, /somedir/tempを除外
*/temp*

# rootから2階層以下のサブディレクトリ内で、 temp で始まる名前のファイルやディレクトリを除外
# ex. /somedir/subdir/temporary.txt を除外
*/*/temp*

# ルートディレクトリ内でtempと1文字が一致する名前のファイルやディレクトリを除外
# ex. /tempa,/tembを除外
temp?
```

### 例外

"!"で始まる行は除外対象の例外として指定されます。
ただし、他の行をみて矛盾がある場合には最終行のほうが優先されます。

- 例 1

```Docker
!README*.md
README-secret.md
```

README-secret.md が!README\*.md より後にあるので、README-secret.md は除外対象となり、README で始まる md ファイルは除外対象にはなりません。

- 例 2

```Docker
README-secret.md
!README*.md
```

!README\*.md が README-secret.md より後にあるので、README-secret.md も含む README で始まる md ファイルはすべて除外対象となりません。

.dockerignore ファイルを使うと Dockerfile と.dockerignore ファイルも除外対象にすることができます。除外設定しても、構築処理で必要なためデーモンに送信されますがADD命令とCOPY命令でイメージにコピーされません。

## 参考

https://docs.docker.jp/engine/reference/builder.html?highlight=dockerignore#dockerignore
