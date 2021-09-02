---
title: "PHPの基本的な書き方"
emoji: "🐣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [PHP, 初心者]
published: true
---

:::message
PHPはサーバサイドで動くので事前にサーバを起動する必要があります。Macの場合は[MAMP](https://www.mamp.info/en/mac/)をインストール^[無料です]すると動作確認できます。
:::

PHPはhtmlファイルの中に記述することができ、PHPの処理を記述するときは<?php ?>の中で処理を書きます。変数を使うときは頭に「$」をつけ、echoで表示することができます。

```php
<!DOCTYPE html>
<head><title>テスト</title></head>
<body>
    <?php 

    // セミコロンが必要
    echo "test"; 

    // 改行される(<br />タグが挿入される)
    echo nl2br("\n");   

    // 変数は$が必要
    $hoge = 3;
    echo hoge;

    ?>
</body>
```

## 実行結果

![実行結果](https://gyazo.com/aa7a105f343e8ed5482e17697d836020.png)
