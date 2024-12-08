---
title: "SwaggerでAPI仕様書を作成してみた"
emoji: "📚"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [backend, swagger, api]
published: true
---

[Swagger](https://swagger.io/)は OpenAPI の仕様に沿って RestAPI の設計を文書にまとめることができるオープンソースのツールです。主要なツールは下記のとおりです

- Swagger Editor
- Swagger UI
- Swagger Codegen
- Swagger Editor Next (beta)
- Swagger Core
- Swagger Parser
- Swagger APIDom

Swagger Editor を使うと準備することもなくブラウザ上で記載することもできますが
GitHub で管理したいため VS Code で記載します。

## 準備

ブラウザで設定した API を確認する

1. VS Code の拡張機能[Swagger Viewer](https://marketplace.visualstudio.com/items?itemName=Arjun.swagger-viewer)をインストール

2. VS Code の設定から Preview In Browser を有効にする

[![Image from Gyazo](https://i.gyazo.com/99aeb2a6178caeda15549d3cead94832.png)](https://gyazo.com/99aeb2a6178caeda15549d3cead94832)

3. 「Cmd」+「Shift」+「P」で Preview Swagger を選択

[![Preview Swagger](https://i.gyazo.com/1843696d30c289e94bb6ab537b355be1.png)](https://gyazo.com/1843696d30c289e94bb6ab537b355be1)

## サンプル

Swagger は yaml 形式もしくは JSON 形式で記載します。

:::message

yaml はコメントを書くことができ、JSON より可読性があるため yaml で書くことをオススメします

:::

### プレビュー画面

[![API](https://i.gyazo.com/863f1c75eb28d12991696fe7902fed31.png)](https://gyazo.com/863f1c75eb28d12991696fe7902fed31)

### サンプルファイル

```
openapi: 3.0.1
info:
  title: User Management API
  description: API to demonstrate CRUD operations.
  version: "1.0.0"
servers:
  - url: http://localhost:3000/api
    description: Local server

paths:
  /users:
    get:
      summary: Retrieve all users
      description: Fetches a list of all users in the system.
      responses:
        200:
          description: A list of users.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'

    post:
      summary: Add a new user
      description: Creates a new user in the system.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserInput'
      responses:
        201:
          description: User created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'

  /users/{userId}:
    get:
      summary: Get user by ID
      description: Retrieves the details of a specific user by their ID.
      parameters:
        - name: userId
          in: path
          required: true
          description: The ID of the user to retrieve.
          schema:
            type: string
      responses:
        200:
          description: User found.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        404:
          description: User not found.

    put:
      summary: Update a user
      description: Updates the information of a specific user.
      parameters:
        - name: userId
          in: path
          required: true
          description: The ID of the user to update.
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserInput'
      responses:
        200:
          description: User updated successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        404:
          description: User not found.

    delete:
      summary: Remove a user
      description: Deletes a specific user from the system.
      parameters:
        - name: userId
          in: path
          required: true
          description: The ID of the user to delete.
          schema:
            type: string
      responses:
        204:
          description: User deleted successfully.
        404:
          description: User not found.

components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the user.
        name:
          type: string
          description: Name of the user.
        email:
          type: string
          description: Email address of the user.

    UserInput:
      type: object
      properties:
        name:
          type: string
          description: Name of the user.
          example: Jane Doe
        email:
          type: string
          description: Email address of the user.
          example: jane.doe@example.com
```

## メリット・デメリット

### メリット

- 書きかたが統一されている
  OpenAPI の仕様に沿って書かないといけないので、人によって書きかたが違うことは発生しないので、可読性が上がるのがよいと感じました。
- Git で管理できる
  yaml で記載しているので GitHub でコミット履歴を追いかけることができるのが便利だと思いました。

### デメリット

- 学習コストがかかる
  ネットで調べてなんとなく書けるようにはなりましたが、パラメータの意味やベストプラクティスなどを理解するためには、もっと勉強する必要があると感じました。

## その他

LT 会で記事の内容を話したので共有します。

https://speakerdeck.com/morleyjp/05

## 参考

https://swagger.io/docs/specification/v3_0/about/
https://www.aeyescan.jp/blog/openapi/
https://swagger.io/specification/
