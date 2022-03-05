---
title: "S3のライフサイクルの定義方法について"
emoji: "👼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AWS, S3]
published: true
---

## ライフサイクルについて

S3 にライフサイクルを設定すると一定期間後にオブジェクトを削除したり、別のストレージクラスに移行したりできます。
ライフサイクルは Amazon S3 コンソール、REST API、AWS SDK、AWS CLI で設定でき、下記のように xml で定義されます。

```xml
<!-- https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/lifecycle-configuration-examples.htmlより引用 -->
<LifecycleConfiguration>
  <Rule>
    <ID>Archive all object same-day upon creation</ID>
    <Filter>
      <Prefix></Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Transition>
      <Days>0</Days>
      <StorageClass>S3 Glacier Flexible Retrieval</StorageClass>
    </Transition>
  </Rule>
</LifecycleConfiguration>
```

他の例も[公式ドキュメント](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/lifecycle-configuration-examples.html)に記載があります。

## 定義ファイルについて

### ID 要素

最大 1000 コのルールが作成できます。

### Status 要素

Enabled または Disabled の値を取ります。
Disabled の場合はアクションを実行しません。

### Filter 要素

どのオブジェクトに対してライフサイクルを設定するかを定義できます。
空の場合はすべてのオブジェクトに対して定義されます。
複数のフィルターを組み合わせる場合は\<AND>を使います。
フィルターするときは\<Filter>の子要素に\<Prefix>または\<Tag>を使います。

```xml
 <LifecycleConfiguration>
    <Rule>
        <Filter>
          <And>
             <Prefix>key-prefix</Prefix>
             <Tag>
                <Key>key1</Key>
                <Value>value1</Value>
             </Tag>
             <Tag>
                <Key>key2</Key>
                <Value>value2</Value>
             </Tag>
              ...
          </And>
        </Filter>
        <Status>Enabled</Status>
        transition/expiration actions.
    </Rule>
</LifecycleConfiguration>
```

### ライフサイクルアクションについて

どのようなアクションを取るか定義できます。

#### Transition

別のストレージクラスに移行する場合に指定します。
バージョニング対応のバケットの場合は最新のオブジェクトバージョンに適用されます。
以前のバージョンの場合は NoncurrentVersionTransition を指定します。

#### Expiration

ルールで指定されたオブジェクトを有効期限切れにします。
バージョニングが非対応のバケットの場合はオブジェクトが完全に削除されます。

#### NoncurrentVersionTransition

指定したストレージクラスに移行するタイミングを指定します。

#### NoncurrentVersionExpiration

最新でないオブジェクトを永続的に削除するタイミングを指定します。

#### その他

他にも AbortIncompleteMultipartUpload、ExpiredObjectDeleteMarker があります。

## S3 の時間設定について

移行ルールが 3 日のときに、あるオブジェクトが 2022 年 3 月 5 日午前 10 時 30 分 (UTC) に作成されると、オブジェクトの移行日は 2022 年 3 月 9 日 0 時 0 分 (UTC)となります。
つまり、時間部分は 0 時 0 分(UTC)に丸められてしまいます。

## 参考

[ストレージのライフサイクルの管理](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)

[ライフサイクル設定の要素](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/intro-lifecycle-rules.html)
