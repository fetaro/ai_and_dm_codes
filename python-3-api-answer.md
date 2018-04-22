
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

    2018-04-23 00:00:00+09:00の気温は16.629999999999995度、天気はMist、風の強さは2.6m/sです。
    

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

    4月23日月曜日0時
    
    4月23日月曜日0時の気温は16度、天気は霧、風の強さは2.6m/sです。
    
