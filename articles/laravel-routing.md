---
title: "Laravelを使ったルーティング方法"
emoji: "🛣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Laravel]
published: true
---

## Laravelのルーティングについて

LaravelではMVCモデル[^1]というアーキテクチャスタイルを採用しています。
まずはルーティングファイルから別のファイルへ遷移させます。
そのとき直接、Viewファイルへ遷移させて表示を行うかControllerファイルへ遷移させるかをルーティングファイルから指定することができます。

[^1]:Model, View, Controllerの略でロジックの部分(Model)と表示する部分(View)を分けて記述することが可能です。

## 実行環境

Laravel ver 8.58.0
PHP ver 7.3.24
## 書き方

Controllerに遷移させる場合は、事前にTestControllerクラスとTestControllerにindexメソッドをそれぞれ定義しておく必要があります。

```php:resources/routes/web.php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\TestController;
// viewへ直接遷移させるとき
// パスが「/」のときwelcome.blade.phpファイルの内容を表示する
Route::get('/', function(){
    return view('welcome');
});

// Controllerに遷移させたいとき
// tests/testにアクセスすると
// TestControllerクラスのindexメソッドが呼び出されます
Route::get('tests/test', [TestController::class, 'index']);
```

:::message
バージョン7までだったら下記の書き方でもOKです。
Route::get('tests/test','TestController@index');
:::

### ハマったところ

バージョン8.x環境で、例のように書いても
```bash
Target class [○○Controller] does not exist.
```
というエラーが起きました。
エラーの原因は下記のように"App"のところが大文字か小文字かの違いでした。
```php
// 正解
use App\Http\Controllers\TestController;

// 間違い
use app\Http\Controllers\TestController;
```


## パスについて

下記コマンドを入力するとサーバが起動します。
```bash
php artisan serve
```

サーバ起動に成功すると下記のように表示されます。
```bash
Starting Laravel development server: http://127.0.0.1:8000
```

パスが「/」のときはURLが http://127.0.0.1:8000 となります。
パスが「tests/test」のときはURLが http://127.0.0.1:8000/tests/test となります。

## 参考

https://www.tairaengineer-note.com/laravel-error-target-class-does-not-exist/

https://readouble.com/laravel/8.x/ja/upgrade.html

https://readouble.com/laravel/8.x/ja/routing.html
