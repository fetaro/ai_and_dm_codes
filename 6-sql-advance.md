
### テーブルの結合

usersテーブルの他にzipsテーブルも作る

```sql
CREATE TABLE zips (
  zip VARCHAR(7) PRIMARY KEY,
  name VARCHAR(50)
);
```

データを入れる

```sql
INSERT INTO zips VALUES("1420043","東京都 品川区 二葉");
INSERT INTO zips VALUES("1400013","東京都 品川区 南大井");
INSERT INTO zips VALUES("1400004","東京都 品川区 南品川");
INSERT INTO zips VALUES("1400003","東京都 品川区 八潮");
INSERT INTO zips VALUES("1420042","東京都 品川区 豊町");
```

データを見る
```sql
SELECT * FROM zips;
```

usersとzipsを結合して表示する

```sql
SELECT * FROM users 
	INNER JOIN zips  -- どのテーブルと結合するか
	ON users.zip = zips.zip -- 結合条件 
	;
```

* INNER JOINは両方のテーブルで条件が一致した行のみを表示する

```sql
SELECT * FROM users
	LEFT JOIN zips 
	ON users.zip = zips.zip 
	;
```

* LEFT JOINならば左側のテーブル(つまりusers)の行は全部表示する


