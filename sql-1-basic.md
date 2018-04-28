### スキーマを作る

testというスキーマを作る

```sql
create schema test character set 'utf8';
```

* ` character set 'utf8'` は文字コードをUTF8にすることの指定
* かならず`;`で終わる必要あり

スキーマを選択

```sql
use test ;
```

### テーブルを作る

```sql
create table user (
  id int, 
  name varchar(20), 
  sex varchar(1),
  age int, 
  zip varchar(7)
);
```

* intは整数
* varchar(20)は20文字の文字列

### データを挿入する

```sql
insert into test.user values(1,"Tetsutaro Watanabe","M",35,"1420042");
```

```sql
insert into test.user values(2,"Taro Yamada","M",30,"1420043");
insert into test.user values(3,"Hanako Suzuki","F",28,"1420050");
```

### データを参照する

```sql
select * from user;
```

## サンプルデータのロード

データのダウンロード：　https://drive.google.com/file/d/1NDDcMcRjjfNiWm42jqPVBRpNAXOzZ4id/view?usp=sharing

