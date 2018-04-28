### はじめに

* 大文字と小文字は区別しない
* 

### スキーマを作る

testというスキーマを作る

```sql
CREATE SCHEMA test CHARACTER SET 'utf8';
```

* ` CHARACTER SET 'utf8'` は文字コードをUTF8にすることの指定
* かならず`;`で終わる必要あり

スキーマを選択

```sql
USE test ;
```

### テーブルを作る

```sql
CREATE TABLE user (
  id INT PRIMARY KEY, 
  name VARCHAR(20), 
  sex VARCHAR(1),
  age INT, 
  zip VARCHAR(7)
);
```

* INTは整数
* PRIMARY KEY は主キーを指定
* VARCHAR(20)は20文字の文字列

### データを挿入する

```sql
INSERT INTO test.user VALUES(1,"Tetsutaro Watanabe","M",35,"1420042");
```

```sql
INSERT INTO test.user VALUES(2,"Taro Yamada","M",30,"1420043");
INSERT INTO test.user VALUES(3,"Hanako Suzuki","F",28,"1420050");
```

### データを参照する

テーブル全体を参照

```sql
SELECT * FROM user;
```

列の絞り込み

```sql
SELECT name,age FROM user;
```

行の絞り込み

```sql
SELECT * FROM user WHERE id = 2; 
```

### データを更新する

```sql
UPDATE user 
SET age = 36
WHERE id = 1
;
```


## サンプルデータのロード

データのダウンロード：　https://drive.google.com/file/d/1NDDcMcRjjfNiWm42jqPVBRpNAXOzZ4id/view?usp=sharing

