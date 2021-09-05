---
title: "PHPの型について"
emoji: "👔"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [PHP, 型]
published: true
---

## TL;DR
PHPの型についてわかります。var_dumpの使い方やsettype()関数を使った型を強制的に変更する方法についてわかります。

## 型

phpでは実行するときに自動で型を決定[^1]します。
下記10種類の型があります。

[^1]:PHP7.4.0以降関数のパラメータや戻り値、クラスのプロパティに対して[型を宣言することができる](https://www.php.net/manual/ja/language.types.declarations.php)ようになりました。

- 4種類のスカラー型:
論理値 (bool)
整数 (int)
浮動小数点数 (float, double も同じ)
文字列 (string)

- 4 種類の複合型:
配列 (array)
オブジェクト (object)
callable
iterable

- 2 種類の特別な型:
リソース (resource)
ヌル (NULL)

## var_dumpの使い方

メモリなどに記録された内容を表示することを**ダンプ**といいます。
var_dump関数を使うことでダンプする(=値や型を知る)ことができます。
使い方はvar_dumpの引数にダンプしたい変数を指定すればOKです。

```php
<?php
$b = 3.1;
$c = true;
var_dump($b, $c);
// 出力結果:float(3.1) bool(true)
?>
```

## キャスト

ある特定の型として評価したいときに、変数の前に評価しようとする型をカッコで囲むことで強制的に型を特定の型として評価することができます。この方法を**キャスト**と呼びます。
文字列の場合は二重引用符("")で括ることでキャストができます。

- キャストのやり方
```php
<?php
$foo = 10;   // $foo は整数です
$bar = (boolean) $foo;   // $bar はbooleanです
?>
```
- 文字列の場合
```php
<?php
$foo = 10;            // $foo は整数です
$str = "$foo";        // $str は文字列です
$fst = (string) $foo; // $fst も文字列です

// これは、"they are the same"を出力します
if ($fst === $str) {
    echo "they are the same";
}
?>
```

## settypeを使った型の変更

settype()関数を使うと指定した変数の型に変更できます。

### 定義
```php
settype(mixed &$var, string $type): bool
```

varにtypeで指定した型をセットします。

### 返り値
成功:true
失敗:false

### 使い方
```php
<?php
$foo = "5bar"; // string
$bar = true;   // boolean

settype($foo, "integer"); // ここでは、$foo は 5です (整数)
settype($bar, "string");  // ここでは、$bar は "1" です (文字列)
?>
```

## 参考

https://www.php.net/manual/ja/language.types.php

