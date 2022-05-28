---
title: "cherry-pickで特定のコミットを取り込む"
emoji: "🍒"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [git]
published: true
---

## cherry-pick の使い方

cherry-pick でコミット番号を指定することで特定のコミットを取り込むことができます。
別ブランチのあるコミットを取り込みたいが、何らかの理由で merge して取り込むことができないときなどに使用すると便利です。

```bash
git cherry-pick commit_id
```

## コミット ID の調べ方

コミット番号を調べるには git log を使います。
別ブランチにコミット履歴がある場合は git branch を使って移動する必要があります。

```bash
git log
```

```bash
commit 8949b7294942d7683badc7edgf505e7af6f91103f (HEAD -> develop, origin/develop)
Author: author_name <abc@example.com>
Date:   Thu May 5 11:29:30 2022 +0900

    second_commit_message

commit 2cb6f84855aa7ab75g69e4b4f1ff260c273ad123
Author: author_name <abc@example.com>
Date:   Thu May 5 10:49:59 2022 +0900

    first_commit_message
```

> commit 8949b7294942d7683badc7edgf505e7af6f91103f (HEAD -> develop, origin/develop)

の 8949b7294942d7683badc7edgf505e7af6f91103f がコミット ID です。

:::message
コミット ID は VS Code や GitHubDesktop などのクライアントツールを使って視覚的に調べることもできます。
:::

コミット ID を調べた後は取り込みたいブランチに移動して cherry-pick しましょう。
