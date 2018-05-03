## 演習4-1の答え

テーブルの作成

```sql
CREATE TABLE user2 (
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
INSERT INTO user2 VALUES(1,"Tetsutaro Watanabe","M",35,"1420042","fetaro@hoge.com");
INSERT INTO user2 VALUES(2,"Taro Yamada","M",30,"1420043","yamada@hoge.com");
INSERT INTO user2 VALUES(3,"Hanako Suzuki","F",28,"1420050","suzuki@hoge.com");
```

データの参照

```sql
SELECT * FROM user2;
```

## 演習4-2の答え

### 従業員の数は？

```sql
USE employees;
SELECT COUNT(*) FROM employees;
'300024'
```

### 従業員の男女の数は？


```sql
select count(*) from employees where gender = 'M';
'179973'

select count(*) from employees where gender = 'F';
'120051'

```

### 給料の一番多い人の、給料、社員番号、名前は？


一番多い給与

```sql
select max(salary) from salaries ;

'158220'

```

一番給与が多い人の社員番号

```sql
select emp_no from salaries where salary = 158220;

'43624'

```

社員の名前

```sql
SELECT first_name, last_name FROM employees WHERE emp_no = 43624;

'Tokuyasu', 'Pesch'

```
