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
CREATE TABLE user (
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
INSERT INTO user VALUES(1,"Tetsutaro Watanabe","M",35,"1420042");
```

もう2行挿入

```sql
INSERT INTO user VALUES(2,"Taro Yamada","M",30,"1420013");
INSERT INTO user VALUES(3,"Hanako Suzuki","F",28,"1420012");
```

idは主キーであり、同じidを持つ行は挿入できない。

```sql
INSERT INTO user VALUES(3,"Jiro Kato","M",40,"1420003");
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

件数の取得

```sql
SELECT COUNT(*) FROM user;
```

条件を指定した件数の絞り込み

```sql
SELECT COUNT(*) FROM user WHERE age < 30;
```

値の最大を取得

```sql
SELECT MAX(age) FROM user;
```

他にも　最小`MIN()`,平均 `AVG()`, 最大`SUM()`　などの関数がある。


### データを更新する

```sql
UPDATE user 
SET age = 36
WHERE id = 1
;
```

### データを削除する

```sql
DELETE user 
WHERE id = 2
;
```

```sql
DELETE FROM user 
WHERE id = 2
;
```

### テーブルを消す

```sql
DROP TABLE user;
```

### 演習4-1

* 先ほど作成したuserテーブルに、e-mailアドレスも格納できるようにした`user2`を作成せよ。
* e-mailアドレスのデータ型は`文字列50文字`である。
* 作成したテーブルに以下のデータを挿入せよ。

```sql
1,"Tetsutaro Watanabe","M",35,"1420042","fetaro@hoge.com";
2,"Taro Yamada","M",30,"1420013","yamada@hoge.com";
3,"Hanako Suzuki","F",28,"1420012","suzuki@hoge.com";
```

### 余談
ちなみに、「hoge」という言葉はIT関係者が良く使う言葉であり、とりあえず適当な文字列を書きたいときに「hoge」とかく。
「hoge」の他にも「bar」が良く使われる。

### テーブルの結合

userテーブルの他にzipテーブルも作る

```sql
CREATE TABLE zips (
  zip VARCHAR(7) PRIMARY KEY,
  name VARCHAR(50)
);
```

データを入れる

```sql
INSERT INTO zips VALUES("1420042","東京都 品川 二葉");
INSERT INTO zips VALUES("1400013","東京都 品川区 南大井");
INSERT INTO zips VALUES("1400004","東京都 品川区 南品川");
INSERT INTO zips VALUES("1400003","東京都 品川区 八潮");
INSERT INTO zips VALUES("1420042","東京都 品川区 豊町");
```

データを見る
```sql
SELECT * FROM zips;
```

```sql
SELECT * FROM user 
	INNER JOIN zips 
 ON user.zip = zips.zip ;
```

## 集計の練習

### サンプルデータのロード

データのダウンロード：　https://drive.google.com/file/d/1NDDcMcRjjfNiWm42jqPVBRpNAXOzZ4id/view?usp=sharing

### サンプルデータのインポート

メニューからServer → Data Import → Import from Self-Contained File → 解凍したsample.sql　を指定して Start Import → Import Completedになることを確認

左のSCHEMASの更新ボタンを押し、employeesという名前のスキーマがあればOK

### データを見る

集計・分析・機械学習・AI、何をするにしてもまずはデータを知ることが第一歩

### 演習4-2

employeesスキーマには、とある会社の社員、給与、所属部署の情報が入っている。
データを見て以下の問いに答えよ。

* 従業員の数は？
* 従業員の男女の数は？
* 給料の一番多い人の、給料、社員番号、名前は？

ヒント：従業員はemployeesテーブル、給与はsalariesテーブルにある
