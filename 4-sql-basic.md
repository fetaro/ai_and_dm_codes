## SQLの基礎

### はじめに

* 大文字と小文字は区別しない
* 右側のページにSQLを書く
  * 稲妻マークを押すとページ全体が実行される
  * 稲島+1マークを押すと、選択した箇所を含むセクション「;」までが実行される
* 作成したデータは、左上のSCHEMASのところに表示される。

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
CREATE TABLE users (
  id INT PRIMARY KEY, 
  name VARCHAR(20), 
  gender VARCHAR(1),
  age INT, 
  zip VARCHAR(7)
);
```

* INTは整数
* PRIMARY KEY は主キーを指定
* VARCHAR(20)は20文字の文字列

### データを挿入する

文法

```sql
INSERT INTO テーブル名 VALUES(値の列挙);
```

1行挿入

```sql
INSERT INTO users VALUES(1,"Tetsutaro Watanabe","M",35,"1420043");
```

もう2行挿入

```sql
INSERT INTO users VALUES(2,"Taro Yamada","M",30,"1400013");
INSERT INTO users VALUES(3,"Hanako Suzuki","F",28,"1400012");
```

idは主キーであり、同じidを持つ行は挿入できない。

```sql
INSERT INTO users VALUES(3,"Jiro Kato","M",40,"1420003");
```

```
Error Code: 1062. Duplicate entry '3' for key 'PRIMARY'
```

### コメント

```sql
-- これが1行コメント
```

```sql
/*
これが
複数行
コメント
*/
```

### データを参照する

テーブル全体を参照

```sql
SELECT * FROM users;
```

列の絞り込み

```sql
SELECT name,age FROM users;
```

行の絞り込み

```sql
SELECT * FROM users WHERE id = 2; 
```

件数の取得

```sql
SELECT COUNT(*) FROM users;
```

条件を指定した件数の絞り込み

```sql
SELECT COUNT(*) FROM users WHERE age < 30;
```

比較するときに使える演算子

``` 
演算子	使用例	意味
=	a = b	a と b は等しい
<>	a <> b	a と b は等しくない
!=	a != b	a と b は等しくない
<	a < b	a は b よりも小さい
<=	a <= b	a は b よりも小さいか等しい
>	a > b	a は b よりも大きい
>=	a >= b	a は b よりも大きいか等しい
```

値の最大を取得

```sql
SELECT MAX(age) FROM users;
```

他にも　最小`MIN()`,平均 `AVG()`, 最大`SUM()`　などの関数がある。


### データを更新する

```sql
UPDATE users 
SET age = 36
WHERE id = 1
;
```

### データを削除する


```sql
DELETE FROM users 
WHERE id = 2
;
```

### テーブルを消す

```sql
DROP TABLE users;
```

### 演習4-1

* 先ほど作成したusersテーブルに、e-mailアドレスも格納できるようせよ。
* e-mailアドレスのデータ型は`文字列50文字`である。
* 作成したテーブルに以下のデータを挿入せよ。

```sql
1,"Tetsutaro Watanabe","M",35,"1420043","fetaro@hoge.com";
2,"Taro Yamada","M",30,"1400013","yamada@hoge.com";
3,"Hanako Suzuki","F",28,"1400012","suzuki@hoge.com";
```

## もっと大きいデータで演習

### サンプルデータのロード

データのダウンロード：　https://drive.google.com/uc?authuser=0&id=1NDDcMcRjjfNiWm42jqPVBRpNAXOzZ4id&export=download

### サンプルデータのインポート

メニューからServer → Data Import → Import from Self-Contained File → 解凍したsample.sql　を指定して Start Import → Import Completedになることを確認

左のSCHEMASの更新ボタンを押し、employeesという名前のスキーマがあればOK

### データの構造を見る

集計・分析・機械学習・AI、何をするにしてもまずはデータを知ることが第一歩。これから使うemployeesテーブル、salariesテーブル、の構造を見てみる。

employeesテーブルの構造を見る

```
DESC employees;
```

salariesテーブルの構造を見る

```
DESC salaries;
```

#### データの中身を見る

employeesテーブルの中身を10件見る

```
SELECT * FROM employees LIMIT 10;
```

salariesテーブルの中身を10件見る

```
SELECT * FROM salaries LIMIT 10;
```

### 演習4-2

employeesスキーマにあるデータを見て以下の問いに答えよ。

* 従業員の数は？
* 従業員の男女の数は？
* 今までで給料が一番多い人の、給料、社員番号、名前は？
* 2000/1/1 ~ 2000/12/31の間で最も高かった給料は？

