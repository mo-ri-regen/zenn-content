---
title: "package-lock.jsonとyarn.lockが共存しているときの解決方法"
emoji: "🔐"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [npm, yarn, nextjs]
published: true
---


'npx create-next-app'でnextjsのプロジェクトを作成すると
package-lock.jsonファイルが作成されてしまう。
その後、パッケージをyarnでインストールすると、yarn.lockが作成されてしまう。
![package-lock.jsonとyarn.lockが共存](https://gyazo.com/ca199476f6a108423b624c8ab2432246.pngs)

vercelにデプロイしようとするとwarningが出る。
![vercelにデプロイしようとするとwarningが出る](https://gyazo.com/83db4a16b393f452ff9527952c14f1c5.png)

意訳すると
「プロジェクトにyarn以外で生成されたlockファイル(package-lock.jsonのこと)が見つかった。
同期されていないlock fileによって引き起こされるバージョン[^1]の不一致を避けるためにpackage managerは混ぜない方がいいよ。このwarningを消すには、package-lock.jsonを削除しよう。」
[^1]: resolutionは決心、解決という意味ですがここでは「バージョン」と訳しました。

## 対処法

warningにも書かれている通りパッケージ管理ファイルは1つだけで十分なので、yarnでパッケージ管理する場合はpackage-lock.jsonは削除する。
これだけでいいが、もし1つのプロジェクトに対してnpmのあとにyarnを行っていると、
どのパッケージをyarnでダウンロードしているのかどうか判断できない。
そのときはいったん、node_modulesを削除し、再度必要なパッケージを
yarn addでインストールすればよい。(yarnを使い出したら、そのプロジェクトにはnpmコマンドは使ってはいけない) 
~~nextjsのプロジェクト作るときにyarn使うかnpm使うか選ばせてほしい~~

## 参考

[package-lock.jsonについて](https://docs.npmjs.com/cli/v7/configuring-npm/package-lock-json)
[npmについて](https://www.npmjs.com/)
[yarn.lockについて](https://classic.yarnpkg.com/en/docs/yarn-lock/)