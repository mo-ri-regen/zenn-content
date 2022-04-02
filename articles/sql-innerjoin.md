---
title: "INNER JOINを使って内部結合する書き方"
emoji: "🔗"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [SQL]
published: true
---

複数のテーブルを結合させて 1 つのテーブルとして操作したいときは INNER JOIN を使います。
また、3 つ以上結合するときは INNER JOIN を繰り返し使うことで結合できます。

列名を指定するときは「テーブル名.カラム名」をすると指定したテーブルのカラム名を選択できます。

## 構文

### 2 つのテーブルを結合

```sql
SELECT table1.column_name, table2.column_name
FROM table1
INNER JOIN table2
ON 結合条件
WHERE 抽出条件
```

### 3 つ以上のテーブルを結合

```sql

select table1.column_name
       ,table2.column_name
       ,table3.column_name
       ,...
FROM   table1
INNER JOIN table2
ON 結合条件
INNER JOIN table3
ON 結合条件
INNER JOIN table4
ON 結合条件
  :
where 抽出条件
```

## 例

### テーブル

下記のテーブルに対して INNER JOIN で結合してみます。

#### fruits テーブル

| id  | name   |
| --- | ------ |
| 1   | apple  |
| 2   | orange |
| 3   | banana |

#### info テーブル

| id  | fruits_id | prices | origin      |
| --- | --------- | ------ | ----------- |
| 1   | 1         | 300    | Japan       |
| 2   | 1         | 200    | America     |
| 3   | 2         | 400    | China       |
| 4   | 3         | 500    | China       |
| 5   | 3         | 100    | Philippines |
| 6   | 3         | 150    | Japan       |

### INNER JOIN を使った SQL 文

```sql
SELECT fruits.name
       ,info.prices
       ,info.origin
FROM   fruits
INNER JOIN info
ON    fruits.id = info.fruits_id
WHERE info.origin = 'Japan';
```

### 実行結果

| name   | prices | origin |
| ------ | ------ | ------ |
| apple  | 300    | Japan  |
| banana | 150    | Japan  |

### 実行環境

[dbfiddle](https://dbfiddle.uk/)
MySQL 8.0
