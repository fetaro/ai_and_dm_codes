# SQLの応用

## データの準備

### データのダウンロード

以下のCSVファイルをダウンロードする

* [hotel.csv](data/hotel.csv)
* [reserve.csv](data/reserve.csv)
* [customer.csv](data/customer.csv)

注意！ダウンロードしたファイルは、日本語を含まないパスに配置すること。

* NG: `C:\Users\渡部徹太郎\Downlaods\hotel.csv`
* OK: `C:\data\hoge.csv`

### スキーマの作成

```sql
CREATE DATABASE myhotel;
USE myhotel;
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


### データのロード

```sql

LOAD DATA LOCAL INFILE '(ダウンロードディレクトリ)/reserve.csv' INTO TABLE reserve FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 LINES;

LOAD DATA LOCAL INFILE '(ダウンロードディレクトリ)/hotel.csv' INTO TABLE hotel FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 LINES;

LOAD DATA LOCAL INFILE '(ダウンロードディレクトリ)/customer.csv' INTO TABLE customer FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 LINES;

```

注意： Windwosの場合'\'は、`\\`のようにバックスラッシュ二つで表す `'C:\\Users\\fetaro\\Downloads\\reserve.csv'`

注意：` warning(s): 1265 Data truncated for column 'home_longitude' at row 1 `のような警告が出ても問題ない

### データが挿入されたことの確認

```sql
USE myhotel;
SELECT count(*) FROM reserve;
-- 4030と表示される
SELECT count(*) FROM hotel;
-- 300と表示される
SELECT count(*) FROM customer;
-- 1000と表示される
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

```sql
SELECT
    customer_id, total_price
FROM
    reserve
ORDER BY total_price DESC; -- DESCで降順
```


### 集計

客ごとの利用回数を集計

```sql
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

結合すると、列名がどちらのテーブルか明示する必要

分析しやすいように、列に別名をつける

```sql
SELECT
    reserve.customer_id,
    reserve.hotel_id,
    reserve.total_price,
    reserve.people_num ,
    customer.age AS cus_age, -- cus_ageという別名
    customer.sex AS cus_sex -- cus_sexという別名
FROM
    reserve
INNER JOIN customer
ON reserve.customer_id = customer.customer_id
;
```

### 演習6-2

* reserveテーブルにhotelテーブルを結合してすべての列を表示せよ
* 結合したテーブルから、列を、地域(hotel.big_area_name)と売上(reserve.total_price)だけにせよ


### 演習6-3

どの地域(hotel.big_area_name)が最も売り上げているか、売上の高い順に表示せよ。
その際、売上はsalesという列名にせよ。

ヒント：地域でグルーピングする

### 3つのテーブルを結合する

```sql
SELECT
    *
FROM
    reserve
INNER JOIN hotel
ON reserve.hotel_id = hotel.hotel_id
INNER JOIN customer
ON reserve.customer_id = customer.customer_id;
```

### 演習6-4

地域(hotel.big_area_name)ごと、年代ごと(10代、20代・・・）に、売り上げの高い順に表示せよ

ヒント：年代ごとの集計は以下の様に行う

```sql
SELECT
    (customer.age DIV 10) * 10 AS age_range, -- 10で割った商に10をかけることにより、年代を計算し、age_rangeという名前を付ける。
    SUM(reserve.total_price)
FROM
    customer
INNER JOIN reserve
ON reserve.customer_id = customer.customer_id
GROUP BY age_range
;

```
