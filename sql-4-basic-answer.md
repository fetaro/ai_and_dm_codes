## 演習4-1の答え

テーブルの作成

```sql
CREATE TABLE users (
  id INT PRIMARY KEY, 
  name VARCHAR(20), 
  gender VARCHAR(1),
  age INT, 
  zip VARCHAR(7),
  email VARCHAR(50)
);
```

データの挿入

```sql
INSERT INTO users VALUES(1,"Tetsutaro Watanabe","M",35,"1420043","fetaro@hoge.com");
INSERT INTO users VALUES(2,"Taro Yamada","M",30,"1400013","yamada@hoge.com");
INSERT INTO users VALUES(3,"Hanako Suzuki","F",28,"1400012","suzuki@hoge.com");
```

データの参照

```sql
SELECT * FROM users;
```

## 演習4-2の答え

### 従業員の数は？

SQL

```sql
USE employees;
SELECT COUNT(*) FROM employees;
```

実行結果

```
300024
```

### 従業員の男女の数は？

SQL

```sql
select count(*) from employees where gender = 'M';
select count(*) from employees where gender = 'F';
```

実行結果

```
179973
120051
```


### 給料の一番多い人の、給料、社員番号、名前は？


一番多い給与

SQL

```sql
select max(salary) from salaries ;
```

実行結果

```
158220
```

一番給与が多い人の社員番号

SQL

```sql
select emp_no from salaries where salary = 158220;
```

実行結果

```
43624
```

社員の名前

SQL

```sql
SELECT first_name, last_name FROM employees WHERE emp_no = 43624;
```

実行結果

```
'Tokuyasu', 'Pesch'
```

