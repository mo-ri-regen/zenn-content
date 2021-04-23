---
title: "gitの概念"
emoji: "😇"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [git]
published: false
---

## Git とは

バージョン管理システム。誰が、いつ、なんの変更を行ったか追いかけることが可能。
スナップショットを記録している。

```
よくあるファイル管理方法

file_20210401.md
file_20210402.md
file_20210403.md
```

### 問題点

- 更新されるたびにファイルが増えていく
- ファイル名を増やしていくので、更新に手間がかかる
- 上記の例の場合、同じ日にファイルの更新履歴を作成することが不可能

## フローチャート

ユーザがローカルで作業した内容(ワークツリー)をステージ(スナップショットを記録するための準備)コミット(スナップショットを記録)する