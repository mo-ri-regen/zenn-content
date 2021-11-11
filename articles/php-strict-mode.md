---
title: "PHPにおけるstrictモードを使った厳密な型宣言"
emoji: "🕵️‍♂️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [php]
published: true
---

以前、PHP の型について[記事](https://zenn.dev/mo_ri_regen/articles/php-about-types)を書きました。今回は型を強制できるというおはなしです。

## strict モードについて

strict モードを有効にすることで厳密な型宣言ができます。
strict モードが有効でないとき、エラーが出ずに実行できてしまうことがあります。[^1]
有効にするには declare 文 に strict_types=1 をセットします。

[^1]: '1'+2 といった「数値に変換できる文字列+数値」に対して、計算結果(この例では 3)が出力されます。

### 例

```php
<?php
// strictモードの有効化
declare(strict_types=1);

function sum(int $a, int $b) {
    return $a + $b;
}

// int(3) という結果が得られる
var_dump(sum(1, 2));

// 引数がintでないためエラーがでる
var_dump(sum(1.5, 2.5));
?>
```

:::message
declare 文では下記のように変数や定数をセットできません

```php
<?php
const STRICT_VALUE = 1;
// これは無効
declare(strict_types=STRICT_VALUE);
?>
```

:::

## strict モードを有効にする必要性

strict モードを有効にしないと、意図しない挙動を起こすことがあります。
たとえば、整数同士の足し算のみ行いたい関数に対して引数として小数を与えたときにエラーが出ず実行されてしまいます。

```php
<?php
function sum(int $a, int $b) {
    return $a + $b;
}

// int(3) という結果が得られる
var_dump(sum(1, 2));

// エラーが出ずにint(3) という結果が得られる
var_dump(sum(1.5, 2.5));
?>
```

## 参考

[declare](https://www.php.net/manual/ja/control-structures.declare.php)
[厳密な型付け](https://www.php.net/manual/ja/language.types.declarations.php#language.types.declarations.strict)
