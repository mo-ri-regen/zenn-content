---
title: "Laravelをインストールしたあと行うべき初期設定"
emoji: "🔧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Laravel]
published: true
---

composerを使ってLaravelをインストールしたあと初めにやっておくべきプロジェクトの設定について話します。

## タイムゾーンの設定

日本に住んでいる場合はタイムゾーンを設定します。

```diff php:config/app.php
- 'timezone' => 'UTC',
+ 'timezone' => 'Asia/Tokyo',
 
- 'locale' => 'en',
+ 'locale' => 'ja',
```

## データベースの文字コード

デフォルトでは絵文字も使える文字コードなのでutf8に変更します。
```diff php:config/database.php
- 'charset' => 'utf8mb4',
- 'collation' => 'utf8mb4_unicode_ci',
+ 'charset' => 'utf8',
+ 'collation' => 'utf8_unicode_ci',
```

## デバッグバーのインストール

デバッグをするときに便利なツールであるデバッグバーをインストールします。

```bash
composer require barryvdh/laravel-debugbar

# 下記コマンドで確認可能
php artisan serve
```

vendor/.envのAPP_DEBUGの値を切り替えることで表示、非表示の設定ができます。
trueで表示、falseで非表示になります。(デフォルトではtrueです。)
```
APP_DEBUG=true
```

APP_DEBUG=trueのときプロジェクトを起動すると下記の画像のようになります。
![APP_DEBUG=trueのとき](https://gyazo.com/1f98e3ccd486a6b9749d15a4563798f3.png)

:::message
キャッシュが残っているせいでAPP_DEBUG=falseにしてもデバッグバーが表示されるときがあります。そのときは下記コマンドでキャッシュとconfigをクリアにします。

```bash
php artisan cache:clear
php artisan config:clear
```

:::