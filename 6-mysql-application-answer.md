## 6-1答え


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

## 6-4の答え

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
