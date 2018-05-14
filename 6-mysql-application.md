# MySQL応用

## データの準備

### データのダウンロード

* [data/hotel.csv](data/hotel.csv)
* [data/reserve.csv](data/reserve.csv)
* [data/customer.csv](data/customer.csv)
* [data/month_mst.csv](data/month_mst.csv)

### スキーマの作成

```sql
CREATE DATABASE myhotel;
```

### テーブル定義 

```sql
CREATE TABLE `customer` (
  `customer_id` text,
  `age` int(11) DEFAULT NULL,
  `sex` text,
  `home_latitude` double DEFAULT NULL,
  `home_longitude` double DEFAULT NULL
);
```

```sql
CREATE TABLE `hotel` (
  `hotel_id` text,
  `base_price` int(11) DEFAULT NULL,
  `big_area_name` text,
  `small_area_name` text,
  `hotel_latitude` double DEFAULT NULL,
  `hotel_longitude` double DEFAULT NULL,
  `is_business` text
);
```

```sql

CREATE TABLE `reserve` (
  `reserve_id` text,
  `hotel_id` text,
  `customer_id` text,
  `reserve_datetime` text,
  `checkin_date` text,
  `checkin_time` text,
  `checkout_date` text,
  `people_num` int(11) DEFAULT NULL,
  `total_price` int(11) DEFAULT NULL
);
```

```sql
CREATE TABLE `month_mst` (
  `year_num` int(11) DEFAULT NULL,
  `month_num` int(11) DEFAULT NULL,
  `month_first_day` text,
  `month_last_day` text
) ;
```


### データのロード

```sql 

LOAD DATA LOCAL INFILE '/Users/01013022/git/ai_and_dm_codes/data/reserve.csv' INTO TABLE reserve FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 LINES;

LOAD DATA LOCAL INFILE '/Users/01013022/git/ai_and_dm_codes/data/hotel.csv' INTO TABLE hotel FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 LINES;

LOAD DATA LOCAL INFILE '/Users/01013022/git/ai_and_dm_codes/data/customer.csv' INTO TABLE customer FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 LINES;

LOAD DATA LOCAL INFILE '/Users/01013022/git/ai_and_dm_codes/data/month_mst.csv' INTO TABLE month_mst FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 LINES;

```

## SQLによる集計

### 並び替え

昇順（値が大きくなる順）に並び替え

```sql
SELECT 
    customer_id, total_price
FROM
    reserve
ORDER BY total_price -- 並び替えたい列を書く
```

降順（値が小さくなっていく順）に並び替え

```
SELECT 
    customer_id, total_price
FROM
    reserve
ORDER BY total_price DESC; --DESCで降順
```


### 集計

客ごとの利用回数を集計

```
SELECT 
    customer_id, 
    COUNT(customer_id) -- まとめた列をカウントする
FROM
    reserve
GROUP BY customer_id  -- まとめたい列を指定
;
```

利用回数の多い客に並べる

```sql
-- 一番の多い利用回数
SELECT 
    customer_id, COUNT(customer_id)
FROM
    reserve
GROUP BY customer_id
ORDER BY COUNT(customer_id) DESC
;
```

### 演習6-1

* 利用回数の多いホテルを、多い順に表示せよ
* 売上の高いホテルを、高い順に表示せよ


### 結合

reserveにcustomerテーブルを結合

```sql
SELECT 
    *
FROM
    reserve
INNER JOIN customer -- 結合するテーブルを指定
ON reserve.customer_id = customer.customer_id -- 結合する条件
;
```

結合した上で、列を絞り込む

```sql
SELECT 
    reserve.customer_id, 
    reserve.hotel_id, 
    reserve.total_price,
    reserve.people_num ,
    customer.age, 
    customer.sex 
FROM
    reserve
INNER JOIN customer 
ON reserve.customer_id = customer.customer_id 
;
```

分析しやすいように、列に別名をつける

```
SELECT 
    reserve.customer_id, 
    reserve.hotel_id, 
    reserve.total_price,
    reserve.people_num ,
    customer.age AS cus_age,
    customer.sex AS cus_sex
FROM
    reserve
INNER JOIN customer 
ON reserve.customer_id = customer.customer_id 
;
```

### 演習6-3 

* reserveテーブルにhotelテーブルを結合してすべての列を表示せよ
* 結合したテーブルから、列を、地域(hotel.big_area_name)と売上(reserve.total_price)だけにせよ


### 演習6-4

どの地域(big_area_name)が最も売り上げているか、売上の高い順に表示せよ。
売上はsalesという列名にせよ。

```sql
SELECT 
    hotel.big_area_name,
    sum(reserve.total_price) AS sales
FROM
    reserve
INNER JOIN hotel
ON reserve.hotel_id = hotel.hotel_id
GROUP BY big_area_name
ORDER BY sales DESC;
;
```
