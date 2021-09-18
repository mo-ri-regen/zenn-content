---
title: "laravelのコントローラの書き方"
emoji: "🕹"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [laravel]
published: true
---

[前回](https://zenn.dev/mo_ri_regen/articles/laravel-routing)でルーティングのさせかたの記事を書きました。
今回はLaravelのコントローラについて書いていきます。

## 作成方法

下記コマンドでコントローラを作成します。

```bash
# UserControllerを作成したいとき
# コントローラだとわかるように末尾にControllerとつける
php artisan make:controller UserController
```

コントローラはapp/Http/Controllersディレクトリに保存されます。

## 遷移させる方法

```php:resources/routes/web.php

// コントローラに遷移させたいとき
// tests/testにアクセスすると
// UserControllerクラスのindexメソッドが呼び出されます
Route::get('tests/test', [UserController::class, 'index']);

// 動的に遷移させたいときは{}で囲む
Route::get('/user/{id}', [UserController::class, 'show']);
```

## 使い方

コントローラを使う場合は、下記のようにルーティングで指定した関数名(ここではindex関数とshow関数)を定義しておく必要があります。

```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    public function index()
    {
        // 'tests/test'にアクセスするとここの処理が実行される
        // 下記の場合、viewのtests/test.blade.phpの処理が実行される
        return view('tests.test');
    }
    /**
     * 指定ユーザーのプロファイルを表示
     *
     * @param  int  $id
     * @return \Illuminate\View\View
     */
    public function show($id)
    {
        return view('user.profile', [
            'user' => User::findOrFail($id)
        ]);
    }    
}
```

## 参考

https://readouble.com/laravel/8.x/ja/controllers.html
