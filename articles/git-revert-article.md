---
title: "間違えてコミットしたときはgit revertで打ち消し!"
emoji: "✏️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Git]
published: false
---

間違えてcommitしたときに打ち消しのコミットを打つことができる😊
:::message alert
コミットを削除せずに打ち消しのコミットを打つ理由。
他の人のリポジトリですでに取り込まれている場合に、コミットを削除してしまうと
整合性が取れず追跡が困難になるため。
:::

## 使い方

直近のコミットを打ち消す場合は"HEAD"と打つ
特定のコミットを打ち消したい場合はコミットのハッシュ値を指定する
--no-commitをつけるとコミットメッセージの入力画面がスキップされ、
コミットメッセージはデフォルトのものが使用される

```zsh
git revert HEAD
```

## 実践

- 準備

1. git init でGitリポジトリの作成
![Gitリポジトリの作成](https://gyazo.com/acec1c0f2b9dd51cafe7f7559bafe656.png)

2. 画像にあるtest.pyについてgit commitでコミットしてみる
![ls](https://gyazo.com/d0c5bd70f46d99b987e417b87f86a798.png)

cf.
ファイルの中身は画像のようになっている
![test.pyの中身](https://gyazo.com/b00a55478021822d8d09cc7c3ace8e78.png)

```zsh
git add test.py
git commit test.py
```

コミットメッセージは適当に入力
![コミットメッセージ](https://gyazo.com/88553a02015cb05859bc789d26c2cc1c.png)

- 実践

1. 現在のコミット状況をgit logを使って確認
![git logで確認](https://gyazo.com/5bbecaf8d46c26d6f90cc880e4ec8e05.png)

2. ファイル編集をしてみる
![ファイル編集](https://gyazo.com/176274094a01c74e2582b6170529b33c.png)

3. ファイル編集したtest.pyについてもう一度git commitでコミットしてみる

    ```zsh
    git add test.py
    git commit test.py
    ```

4. git logでコミットしたことを確認
(change textが最新のコミット)
![git log](https://gyazo.com/a11bc619b58e3f09da4d6a92461b538b.png)

5. git revertでコミットを打ち消す
直前のコミットを打ち消すのでHEADをつける

    ```zsh
    git revert HEAD
    ```

コミットメッセージは適当に入力
![git revertのコミットメッセージ](https://gyazo.com/30263d7d2152d09f07b279cfd5d3b8af.png)
6. 打ち消しできているか確認

ログの確認
Revertというログが残っている👏
![git log](https://gyazo.com/4587aa4ca40937136c2bd3c533a8eb79.png)

ファイルの中身もきちんと最初の中身とおなじになっている😊
![ファイルの中身](https://gyazo.com/2a1b9b66bd4f81159ee74fa12d13ed49.png)

## git resetの違い

git resetはgit commitコマンドが削除されてしまうのに対して、
上記の例で見たようにgit revertは単なる打ち消しのコミットを入れているだけ。
なので、チームで使うときはgit revertで打ち消しのコミットをしたほうがよい

## 参考

- [git revert(公式)](https://git-scm.com/docs/git-revert)

- [SoftwareDesign 2021年7月号(p.10〜p.11)](https://gihyo.jp/magazine/SD/archive/2021/202107)

- [git reset(公式)](https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E3%81%95%E3%81%BE%E3%81%96%E3%81%BE%E3%81%AA%E3%83%84%E3%83%BC%E3%83%AB-%E3%83%AA%E3%82%BB%E3%83%83%E3%83%88%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E8%A9%B3%E8%AA%AC)
