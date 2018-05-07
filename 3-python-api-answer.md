
## 課題3-1の答え


```python
# -*- coding: utf-8 -*-
import requests
import json
from datetime import datetime, timezone, timedelta

api_key = "e6bc6cc0169f020add3b459c0c14c71c"
city = "Tokyo"
response = requests.get("http://api.openweathermap.org/data/2.5/weather?q={0}&appid={1}".format(city,api_key))
json_str = response.text
w_dict = json.loads(json_str)

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

print("{0}の気温は{1}度、天気は{2}、風の強さは{3}m/sです。".format(time,temp,weather,wind_speed))
```

    2018-04-30 22:56:00+09:00の気温は17.980000000000018度、天気はClouds、風の強さは2.6m/sです。
    

## 課題3-2の答え


```python
# -*- coding: utf-8 -*-
import requests
import json
from datetime import datetime, timezone, timedelta

api_key = "e6bc6cc0169f020add3b459c0c14c71c"
city = "Tokyo"
response = requests.get("http://api.openweathermap.org/data/2.5/weather?q={0}&appid={1}".format(city,api_key))
json_str = response.text
w_dict = json.loads(json_str)

# 時刻
unix_time = w_dict["dt"]
JST = timezone(timedelta(hours=+9), 'JST')
time = datetime.fromtimestamp(unix_time,  JST)
youbi = ["月","火","水","木","金","土","日"]
time_str = "{0}月{1}日{2}曜日{3}時".format(time.month, time.day, youbi[time.weekday()] ,time.hour)
print(time_str)

# 摂氏の温度
temp_kerbin = w_dict["main"]["temp"]
temp = int(temp_kerbin - 273.15) #intにすることにより、小数点以下切り捨て

# 天気
discription_dict = {
    "clear sky":"晴れ",
    "few clouds":"曇り時々晴れ",
    "scattered clouds":"曇り",
    "broken clouds":"曇り",
    "shower rain":"曇り時々雨",
    "rain":"雨",
    "thunderstorm":"雷雨",
    "snow":"雪",
    "mist":"霧"
}
weather = discription_dict[w_dict["weather"][0]["description"]]

# 風の強さ
wind_speed = w_dict["wind"]["speed"]

print("{0}の気温は{1}度、天気は{2}、風の強さは{3}m/sです。".format(time_str,temp,weather,wind_speed))
```

    4月30日月曜日22時
    4月30日月曜日22時の気温は17度、天気は曇り、風の強さは2.6m/sです。
    



## 課題3-3の答え



```python
# -*- coding: utf-8 -*-
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

    print('"{0}","{1}","{2}","{3}"'.format(time,temp,weather,wind_speed))
```

    "2018-05-01 00:00:00+09:00","16.29000000000002","Clear","2.66"
    "2018-05-01 03:00:00+09:00","14.520000000000039","Clear","1.77"
    "2018-05-01 06:00:00+09:00","15.400000000000034","Clear","3.57"
    "2018-05-01 09:00:00+09:00","20.960000000000036","Clear","2.41"
    "2018-05-01 12:00:00+09:00","23.223000000000013","Clear","1.66"
    "2018-05-01 15:00:00+09:00","23.872000000000014","Clear","1.51"
    "2018-05-01 18:00:00+09:00","22.10300000000001","Clouds","2.87"
    "2018-05-01 21:00:00+09:00","18.333000000000027","Clouds","3.32"
    "2018-05-02 00:00:00+09:00","16.824000000000012","Clouds","2.67"
    "2018-05-02 03:00:00+09:00","16.55800000000005","Clouds","2.22"
    "2018-05-02 06:00:00+09:00","16.611000000000047","Clear","1.61"
    "2018-05-02 09:00:00+09:00","22.11500000000001","Clear","2.07"
    "2018-05-02 12:00:00+09:00","23.78400000000005","Clear","4.67"
    "2018-05-02 15:00:00+09:00","23.14500000000004","Clouds","5.56"
    "2018-05-02 18:00:00+09:00","20.884000000000015","Clouds","5.93"
    "2018-05-02 21:00:00+09:00","19.862000000000023","Clouds","6.16"
    "2018-05-03 00:00:00+09:00","19.379999999999995","Clouds","6.57"
    "2018-05-03 03:00:00+09:00","18.906000000000006","Rain","7"
    "2018-05-03 06:00:00+09:00","20.122000000000014","Rain","10.21"
    "2018-05-03 09:00:00+09:00","20.406000000000006","Rain","11.36"
    "2018-05-03 12:00:00+09:00","20.886000000000024","Rain","11.34"
    "2018-05-03 15:00:00+09:00","21.555000000000007","Rain","9.79"
    "2018-05-03 18:00:00+09:00","19.222000000000037","Clouds","9.86"
    "2018-05-03 21:00:00+09:00","17.75","Clouds","9.36"
    "2018-05-04 00:00:00+09:00","16.161","Clear","10.35"
    "2018-05-04 03:00:00+09:00","14.947000000000003","Clear","9.78"
    "2018-05-04 06:00:00+09:00","14.79000000000002","Clear","9.56"
    "2018-05-04 09:00:00+09:00","16.75","Clear","9.12"
    "2018-05-04 12:00:00+09:00","18.358000000000004","Clear","9.73"
    "2018-05-04 15:00:00+09:00","18.772000000000048","Clear","9.76"
    "2018-05-04 18:00:00+09:00","17.664000000000044","Clear","9.16"
    "2018-05-04 21:00:00+09:00","16.355000000000018","Clear","7.06"
    "2018-05-05 00:00:00+09:00","15.117000000000019","Clouds","4.81"
    "2018-05-05 03:00:00+09:00","13.288000000000011","Clear","2.53"
    "2018-05-05 06:00:00+09:00","13.052999999999997","Clear","1.32"
    "2018-05-05 09:00:00+09:00","18.170000000000016","Clear","0.61"
    "2018-05-05 12:00:00+09:00","20.114000000000033","Clear","2.01"
    "2018-05-05 15:00:00+09:00","20.753000000000043","Clear","1.86"
    "2018-05-05 18:00:00+09:00","19.595000000000027","Clear","1.71"
    "2018-05-05 21:00:00+09:00","15.071000000000026","Clear","1.71"
    
