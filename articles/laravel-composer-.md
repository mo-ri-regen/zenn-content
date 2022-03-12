---
title: "LaravelにおけるComposerというパッケージ管理ツールについて"
emoji: "🎼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [PHP, laravel, composer]
published: true
---

## Composer とは

PHP の依存関係を管理するツールです。Node.js の npm や Ruby の bundler にインスパイアされたそうです。
公式サイトに指揮者のような画像がある理由は、"composer"は日本語で"作曲"という意味だからだと推測します。
2022 年 3 月 12 日時点で最新バージョンは Composer 2.2 LTS であり、PHP の versions 5.3.2 - 8.1 がサポートされています。

> Composer is not a package manager in the same sense as Yum or Apt are.

と書かれている通り、公式サイトでパッケージマネージャではないと明言されています。

composer.json に下記のように追加したパッケージが記載されます。

```json:composer.json
// https://getcomposer.org/doc/articles/custom-installers.md#composer-jsonより引用
{
    "name": "phpdocumentor/template-installer-plugin",
    "type": "composer-plugin",
    "license": "MIT",
    "autoload": {
        "psr-0": {"phpDocumentor\\Composer": "src/"}
    },
    "extra": {
        "class": "phpDocumentor\\Composer\\TemplateInstallerPlugin"
    },
    "require": {
        "composer-plugin-api": "^1.0"
    },
    "require-dev": {
        "composer/composer": "^1.3"
    }
}
```

## 依存関係の解決

### インストール

```bash
php composer.phar install
```

をすると カレントディレクトリにある composer.json をもとに依存関係を解決し、vendor ディレクトリにインストールします。composer.lock がない場合は作成されます。

```bash
php composer.phar update
```

をすると依存関係に基づいた最新のバージョンを取得します。
Git で commit するとどのバージョンのどのライブラリを使っているか共有できます。

特定のパッケージをアップデートする場合は下記のように指定できます。

```bash
php composer.phar update vendor/package vendor/package2
```

### アンインストール

composer.json からアンインストールするには remove を使います。

```bash
php composer.phar remove vendor/package vendor/package2
```

## 参考

[公式ドキュメント](https://getcomposer.org/)
[GitHub](https://github.com/composer/composer)
