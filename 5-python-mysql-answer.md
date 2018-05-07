## 演習5-1の答え

```Python

# -*- coding: utf-8 -*-
import mysql.connector

# MySQLに接続する
con = mysql.connector.connect(
        host='127.0.0.1',
        db='test',
        user='root',
        password='temutemu' #設定したパスワードを入れる
    )
cur = con.cursor()

data_list = [
        {
                'id': 6,
                'name': 'Shigeru Joshima',
                'gender':'M',
                'age':47,
                'zip':'1420001',
                'email':'joshima@hoge.com'
        },
        {
                'id': 7,
                'name': 'Taichi Kokubun',
                'gender':'M',
                'age':43,
                'zip':'1420001',
                'email':'kokubun@hoge.com'
        },
        {
                'id': 8,
                'name': 'Masahiro Matsuoka',
                'gender':'M',
                'age':41,
                'zip':'1420001',
                'email':'matsuoka@hoge.com'
        },
        {
                'id': 9,
                'name': 'Tomoya Nagase',
                'gender':'M',
                'age':39,
                'zip':'1420001',
                'email':'nagase@hoge.com'
        },
]

for d in data_list:
    # SQLを実行する
    sql = "insert into users values({0}, '{1}', '{2}', {3}, '{4}', '{5}')".format(d['id'],d['name'],d['gender'],d['age'],d['zip'],d['email'])
    cur.execute(sql)

# 変更を確定する
con.commit()

# データベースからの接続をクローズする
cur.close()
con.close()

```

## 演習5-2の答え

```python
# -*- coding: utf-8 -*-

import mysql.connector

# MySQLに接続する
con = mysql.connector.connect(
        host='127.0.0.1',
        db='test',
        user='root',
        password='xxx' #設定したパスワードを入れる
    )
cur = con.cursor()

# APIのデータを取得する(ここからは演習3-3の内容)
import requests
import json
from datetime import datetime, timezone, timedelta
api_key = "e6bc6cc0169f020add3b459c0c14c71c"
city = "Tokyo"
response = requests.get("https://api.openweathermap.org/data/2.5/forecast?q={0}&appid={1}".format(city,api_key))
json_str = response.text
f_dict = json.loads(json_str)

weather_list = f_dict["list"]
for w_dict in weather_list:
    # 時刻
    unix_time = w_dict["dt"]
    JST = timezone(timedelta(hours=+9), 'JST')
    time = datetime.fromtimestamp(unix_time,  JST)

    # 摂氏の温度
    temp_kerbin = w_dict["main"]["temp"]
    temp = temp_kerbin - 273.15

    # 天気
    weather = w_dict["weather"][0]["main"]

    # 風の強さ
    wind_speed = w_dict["wind"]["speed"]

    # SQLを作る
    sql = "insert into forcast values('{0}',{1},'{2}',{3})".format(time,temp,weather,wind_speed)

    # SQLを表示する（デバッグ用）
    print(sql)

    # SQLを実行する
    cur.execute(sql)


# 変更を確定する
con.commit()

# データベースからの接続をクローズする
cur.close()
con.close()
```


## 演習5-3の答え

```sql
CREATE TABLE forcast2(
	  dt DATETIME,
    temp FLOAT,
    wather VARCHAR(40),
    windspeed FLOAT
);
```

```python
# -*- coding: utf-8 -*-

import mysql.connector

# MySQLに接続する
con = mysql.connector.connect(
        host='127.0.0.1',
        db='test',
        user='root',
        password='xxx' #設定したパスワードを入れる
    )
cur = con.cursor()

# APIのデータを取得する(ここからは演習3-3の内容)
import requests
import json
from datetime import datetime, timezone, timedelta
api_key = "e6bc6cc0169f020add3b459c0c14c71c"
city = "Tokyo"
response = requests.get("https://api.openweathermap.org/data/2.5/forecast?q={0}&appid={1}".format(city,api_key))
json_str = response.text
f_dict = json.loads(json_str)

weather_list = f_dict["list"]
for w_dict in weather_list:
    # 時刻
    unix_time = w_dict["dt"]
    JST = timezone(timedelta(hours=+9), 'JST')
    time = datetime.fromtimestamp(unix_time,  JST)

    # 摂氏の温度
    temp_kerbin = w_dict["main"]["temp"]
    temp = temp_kerbin - 273.15

    # 天気
    weather = w_dict["weather"][0]["main"]

    # 風の強さ
    wind_speed = w_dict["wind"]["speed"]

    # 日時をMySQLのDATETIME型に挿入できる形にする
    time_str = time.strftime("%Y-%m-%d %H:%M:%S")

    # SQLを作る
    sql = "insert into forcast2 values('{0}',{1},'{2}',{3})".format(time_str,temp,weather,wind_speed)

    # SQLを表示する（デバッグ用）
    print(sql)

    # SQLを実行する
    cur.execute(sql)


# 変更を確定する
con.commit()

# データベースからの接続をクローズする
cur.close()
con.close()
```
