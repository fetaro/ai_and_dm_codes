## 演習6-1答え


```sql
--利用回数の多いホテルを、多い順に表示せよ
SELECT
    hotel_id, COUNT(hotel_id)
FROM
    reserve
GROUP BY hotel_id
ORDER BY COUNT(hotel_id) DESC;
```

```sql
--売上の高いホテルを、高い順に表示せよ
SELECT
    hotel_id, sum(total_price)
FROM
    reserve
GROUP BY hotel_id
ORDER BY sum(total_price) DESC;
```

## 演習6-2の答え

```sql
-- reserveテーブルにhotelテーブルを結合してすべての列を表示せよ
SELECT
    *
FROM
    reserve
INNER JOIN hotel
ON reserve.hotel_id = hotel.hotel_id
```

```sql
-- 結合したテーブルから、列を、地域(hotel.big_area_name)と売上(reserve.total_price)だけにせよ
SELECT
    hotel.big_area_name,
    reserve.total_price
FROM
    reserve
INNER JOIN hotel
ON reserve.hotel_id = hotel.hotel_id
```

## 演習6-3の答え

```sql
SELECT
    hotel.big_area_name,
    SUM(reserve.total_price) AS sales
FROM
    reserve
INNER JOIN hotel
ON reserve.hotel_id = hotel.hotel_id
GROUP BY hotel.big_area_name
ORDER BY sales DESC
;
```

## 演習6-4の答え

```sql
SELECT
    hotel.big_area_name,
    (customer.age DIV 10) * 10 AS age_range,
    sum(reserve.total_price) AS sales
FROM
    reserve
INNER JOIN hotel
ON reserve.hotel_id = hotel.hotel_id
INNER JOIN customer
ON reserve.customer_id = customer.customer_id
GROUP BY big_area_name, age_range
ORDER BY sales DESC;
;
```
