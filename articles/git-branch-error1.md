---
title: "Gitでデフォルトブランチ名を変えるときにエラーが出た"
emoji: "😫"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Git, エラー]
published: true
---

## 事例

下記コマンドを入力するとエラーが起こる
git branch -M main

```bash
error: refname refs/heads/new_branch not found
```

## 原因

ワークツリーで作業した内容をステージングエリアに追加していないために起こる

## 解決策

git add コマンドでステージングエリアに追加することで解決

## 参考 URL

- git add コマンドとは
  https://www.atmarkit.co.jp/ait/articles/2003/13/news031.html
- 解決策
  https://stackoverflow.com/questions/18382986/git-rename-local-branch-failed
