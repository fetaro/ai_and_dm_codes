
## 事前準備

### 気象情報APIのAPIキーの取得

https://openweathermap.org/price にアクセス

![3-0.png](3-0.png)

Get API Key and Start をクリック

![3-1.png](3-1.png)

University of Tokyoを入力し、教育を選ぶ

![3-2.png](3-2.png)

API Keysのタブを開いてKyesの値をメモする

![3-3.png](3-3.png)

## ディクショナリの復習


```python
colors = {"carrot":"orange", "tomato": "red", "corn":"yellow" }
print(colors)
print(colors["tomato"])
colors["cucumber"] = "green"
print(colors)
```


```python
## 階層の深いディクショナリ
```


```python
user_dict = {"id":10,
            "name":"watanabe",
            "friend_list" : [12,43,60,31],
             "hobby_list" : [
                {"name":"majong",  "year":25},
                {"name":"karaoke", "year":20},
                {"name":"bicycle", "year":5},
             ]
            }
```


```python
print(user_dict["friend_list"])
print(user_dict["friend_list"][3])
print(user_dict["hobby_list"][2])
print(user_dict["hobby_list"][2]["year"])
```

    [12, 43, 60, 31]
    31
    {'name': 'bicycle', 'year': 5}
    5
    

## APIからデータを取得して表示する


```python
import requests

# ここに自分で取得したAPIのキーの値を入れる
# うまく動かない場合は、渡部のキーをそのまま使ってもまあOK
api_key = "e6bc6cc0169f020add3b459c0c14c71c" 

city = "Tokyo"
response = requests.get("http://api.openweathermap.org/data/2.5/weather?q={0}&appid={1}".format(city,api_key))
print(response.text)
```

    {"coord":{"lon":139.76,"lat":35.68},"weather":[{"id":701,"main":"Mist","description":"mist","icon":"50n"}],"base":"stations","main":{"temp":290.15,"pressure":1019,"humidity":67,"temp_min":289.15,"temp_max":292.15},"visibility":16093,"wind":{"speed":2.1,"deg":50},"clouds":{"all":1},"dt":1524409020,"sys":{"type":1,"id":7622,"message":0.0082,"country":"JP","sunrise":1524340757,"sunset":1524388807},"id":1850147,"name":"Tokyo","cod":200}
    

## JSONをディクショナリに変換して表示する


```python
# 今までのプログラムに以下を追記
import json   # JSONライブラリをインポート
json_str = response.text
w_dict = json.loads(json_str)
print(w_dict)
```

    {'coord': {'lon': 139.76, 'lat': 35.68}, 'weather': [{'id': 701, 'main': 'Mist', 'description': 'mist', 'icon': '50n'}], 'base': 'stations', 'main': {'temp': 290.15, 'pressure': 1019, 'humidity': 67, 'temp_min': 289.15, 'temp_max': 292.15}, 'visibility': 16093, 'wind': {'speed': 2.1, 'deg': 50}, 'clouds': {'all': 1}, 'dt': 1524409020, 'sys': {'type': 1, 'id': 7622, 'message': 0.0082, 'country': 'JP', 'sunrise': 1524340757, 'sunset': 1524388807}, 'id': 1850147, 'name': 'Tokyo', 'cod': 200}
    

## ディクショナリをきれいに表示する


```python
# 今までのプログラムに以下を追記
import pprint    # Pretty Printライブラリをインポート
pp = pprint.PrettyPrinter(indent=4)
pp.pprint(w_dict)
```

    {   'base': 'stations',
        'clouds': {'all': 1},
        'cod': 200,
        'coord': {'lat': 35.68, 'lon': 139.76},
        'dt': 1524409020,
        'id': 1850147,
        'main': {   'humidity': 67,
                    'pressure': 1019,
                    'temp': 290.15,
                    'temp_max': 292.15,
                    'temp_min': 289.15},
        'name': 'Tokyo',
        'sys': {   'country': 'JP',
                   'id': 7622,
                   'message': 0.0082,
                   'sunrise': 1524340757,
                   'sunset': 1524388807,
                   'type': 1},
        'visibility': 16093,
        'weather': [   {   'description': 'mist',
                           'icon': '50n',
                           'id': 701,
                           'main': 'Mist'}],
        'wind': {'deg': 50, 'speed': 2.1}}
    

## 時刻を取得


```python
# 今までのプログラムに以下を追記
unix_time = w_dict["dt"]
print(unix_time)
```

    1524409020
    

## UNIXタイムを日本時間で解釈して表示


```python
# 今までのプログラムに以下を追記
from datetime import datetime, timezone, timedelta
JST = timezone(timedelta(hours=+9), 'JST')
time = datetime.fromtimestamp(unix_time,  JST)
print(time)
```

    2018-04-22 23:57:00+09:00
    

## 課題 3-1

時刻、温度、天気、風の強さを取得し、天気予報の日本語文字列を出力せよ

```
出力：2018-04-24 12:00:00+09:00の気温は13.6度、天気はCloud、風の強さは5.1m/sです。
```

ヒント：どこにデータが有るかわからない、データの意味がわからない場合は、データの仕様書 https://openweathermap.org/current を読む

## 課題3-2（時間が余ったら）

天気予報をより流暢な日本語にせよ

出力：4月24日火曜日12時の気温は13度、天気は曇り、風の強さは5.1m/sです。

ヒント：天気の文字列の種類は　https://openweathermap.org/weather-conditions　を見る

## 天気予報の取得

天気予報の取得は `https://api.openweathermap.org/data/2.5/forecast` を使う


```python
# APIの呼び出し
import requests
api_key = "e6bc6cc0169f020add3b459c0c14c71c"
city = "Tokyo"
response = requests.get("https://api.openweathermap.org/data/2.5/forecast?q={0}&appid={1}".format(city,api_key))

# データをJSONにする
import json  
json_str = response.text
f_dict = json.loads(json_str)

# 綺麗に表示
import pprint
pp = pprint.PrettyPrinter(indent=4)
pp.pprint(f_dict)
```

    {   'city': {   'coord': {'lat': 35.6828, 'lon': 139.759},
                    'country': 'JP',
                    'id': 1850147,
                    'name': 'Tokyo',
                    'population': 8336599},
        'cnt': 40,
        'cod': '200',
        'list': [   {   'clouds': {'all': 0},
                        'dt': 1524873600,
                        'dt_txt': '2018-04-28 00:00:00',
                        'main': {   'grnd_level': 1023.61,
                                    'humidity': 77,
                                    'pressure': 1023.61,
                                    'sea_level': 1027.38,
                                    'temp': 296.29,
                                    'temp_kf': 3.98,
                                    'temp_max': 296.29,
                                    'temp_min': 292.309},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 26.5025, 'speed': 1.81}},
                    {   'clouds': {'all': 32},
                        'dt': 1524884400,
                        'dt_txt': '2018-04-28 03:00:00',
                        'main': {   'grnd_level': 1023.52,
                                    'humidity': 71,
                                    'pressure': 1023.52,
                                    'sea_level': 1027.36,
                                    'temp': 296.75,
                                    'temp_kf': 2.98,
                                    'temp_max': 296.75,
                                    'temp_min': 293.766},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'scattered clouds',
                                           'icon': '03d',
                                           'id': 802,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 107.502, 'speed': 0.22}},
                    {   'clouds': {'all': 20},
                        'dt': 1524895200,
                        'dt_txt': '2018-04-28 06:00:00',
                        'main': {   'grnd_level': 1023.97,
                                    'humidity': 63,
                                    'pressure': 1023.97,
                                    'sea_level': 1027.69,
                                    'temp': 295.63,
                                    'temp_kf': 1.99,
                                    'temp_max': 295.63,
                                    'temp_min': 293.641},
                        'rain': {'3h': 0.000695},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10d',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 186.5, 'speed': 4.57}},
                    {   'clouds': {'all': 20},
                        'dt': 1524906000,
                        'dt_txt': '2018-04-28 09:00:00',
                        'main': {   'grnd_level': 1025.56,
                                    'humidity': 62,
                                    'pressure': 1025.56,
                                    'sea_level': 1029.35,
                                    'temp': 293.03,
                                    'temp_kf': 0.99,
                                    'temp_max': 293.03,
                                    'temp_min': 292.04},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'few clouds',
                                           'icon': '02d',
                                           'id': 801,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 179.5, 'speed': 4.65}},
                    {   'clouds': {'all': 0},
                        'dt': 1524916800,
                        'dt_txt': '2018-04-28 12:00:00',
                        'main': {   'grnd_level': 1026.96,
                                    'humidity': 73,
                                    'pressure': 1026.96,
                                    'sea_level': 1030.79,
                                    'temp': 289.808,
                                    'temp_kf': 0,
                                    'temp_max': 289.808,
                                    'temp_min': 289.808},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01n',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 175.5, 'speed': 4.71}},
                    {   'clouds': {'all': 8},
                        'dt': 1524927600,
                        'dt_txt': '2018-04-28 15:00:00',
                        'main': {   'grnd_level': 1027.25,
                                    'humidity': 80,
                                    'pressure': 1027.25,
                                    'sea_level': 1031,
                                    'temp': 289.786,
                                    'temp_kf': 0,
                                    'temp_max': 289.786,
                                    'temp_min': 289.786},
                        'rain': {'3h': 2.5000000000001e-05},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01n',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 185.503, 'speed': 4.56}},
                    {   'clouds': {'all': 0},
                        'dt': 1524938400,
                        'dt_txt': '2018-04-28 18:00:00',
                        'main': {   'grnd_level': 1027.08,
                                    'humidity': 86,
                                    'pressure': 1027.08,
                                    'sea_level': 1030.86,
                                    'temp': 289.608,
                                    'temp_kf': 0,
                                    'temp_max': 289.608,
                                    'temp_min': 289.608},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01n',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 195.002, 'speed': 4.67}},
                    {   'clouds': {'all': 0},
                        'dt': 1524949200,
                        'dt_txt': '2018-04-28 21:00:00',
                        'main': {   'grnd_level': 1028.38,
                                    'humidity': 84,
                                    'pressure': 1028.38,
                                    'sea_level': 1032.22,
                                    'temp': 290.277,
                                    'temp_kf': 0,
                                    'temp_max': 290.277,
                                    'temp_min': 290.277},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 208.002, 'speed': 3.76}},
                    {   'clouds': {'all': 20},
                        'dt': 1524960000,
                        'dt_txt': '2018-04-29 00:00:00',
                        'main': {   'grnd_level': 1029.32,
                                    'humidity': 69,
                                    'pressure': 1029.32,
                                    'sea_level': 1033.1,
                                    'temp': 293.94,
                                    'temp_kf': 0,
                                    'temp_max': 293.94,
                                    'temp_min': 293.94},
                        'rain': {'3h': 0.001075},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10d',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 205.002, 'speed': 4.46}},
                    {   'clouds': {'all': 0},
                        'dt': 1524970800,
                        'dt_txt': '2018-04-29 03:00:00',
                        'main': {   'grnd_level': 1028.85,
                                    'humidity': 65,
                                    'pressure': 1028.85,
                                    'sea_level': 1032.49,
                                    'temp': 294.825,
                                    'temp_kf': 0,
                                    'temp_max': 294.825,
                                    'temp_min': 294.825},
                        'rain': {'3h': 7.5000000000002e-05},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 198.504, 'speed': 6.77}},
                    {   'clouds': {'all': 0},
                        'dt': 1524981600,
                        'dt_txt': '2018-04-29 06:00:00',
                        'main': {   'grnd_level': 1027.77,
                                    'humidity': 62,
                                    'pressure': 1027.77,
                                    'sea_level': 1031.33,
                                    'temp': 294.837,
                                    'temp_kf': 0,
                                    'temp_max': 294.837,
                                    'temp_min': 294.837},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 199.501, 'speed': 7.52}},
                    {   'clouds': {'all': 0},
                        'dt': 1524992400,
                        'dt_txt': '2018-04-29 09:00:00',
                        'main': {   'grnd_level': 1027.76,
                                    'humidity': 69,
                                    'pressure': 1027.76,
                                    'sea_level': 1031.41,
                                    'temp': 293.168,
                                    'temp_kf': 0,
                                    'temp_max': 293.168,
                                    'temp_min': 293.168},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 197.005, 'speed': 7.36}},
                    {   'clouds': {'all': 0},
                        'dt': 1525003200,
                        'dt_txt': '2018-04-29 12:00:00',
                        'main': {   'grnd_level': 1028.9,
                                    'humidity': 78,
                                    'pressure': 1028.9,
                                    'sea_level': 1032.6,
                                    'temp': 291.804,
                                    'temp_kf': 0,
                                    'temp_max': 291.804,
                                    'temp_min': 291.804},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01n',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 198.504, 'speed': 6.61}},
                    {   'clouds': {'all': 32},
                        'dt': 1525014000,
                        'dt_txt': '2018-04-29 15:00:00',
                        'main': {   'grnd_level': 1029.06,
                                    'humidity': 79,
                                    'pressure': 1029.06,
                                    'sea_level': 1032.86,
                                    'temp': 291.31,
                                    'temp_kf': 0,
                                    'temp_max': 291.31,
                                    'temp_min': 291.31},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'scattered clouds',
                                           'icon': '03n',
                                           'id': 802,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 200, 'speed': 5.81}},
                    {   'clouds': {'all': 12},
                        'dt': 1525024800,
                        'dt_txt': '2018-04-29 18:00:00',
                        'main': {   'grnd_level': 1028.69,
                                    'humidity': 81,
                                    'pressure': 1028.69,
                                    'sea_level': 1032.5,
                                    'temp': 290.972,
                                    'temp_kf': 0,
                                    'temp_max': 290.972,
                                    'temp_min': 290.972},
                        'rain': {'3h': 4.9999999999998e-05},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01n',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 197.001, 'speed': 5.16}},
                    {   'clouds': {'all': 20},
                        'dt': 1525035600,
                        'dt_txt': '2018-04-29 21:00:00',
                        'main': {   'grnd_level': 1029.03,
                                    'humidity': 81,
                                    'pressure': 1029.03,
                                    'sea_level': 1032.86,
                                    'temp': 290.96,
                                    'temp_kf': 0,
                                    'temp_max': 290.96,
                                    'temp_min': 290.96},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'few clouds',
                                           'icon': '02d',
                                           'id': 801,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 190.505, 'speed': 4.91}},
                    {   'clouds': {'all': 56},
                        'dt': 1525046400,
                        'dt_txt': '2018-04-30 00:00:00',
                        'main': {   'grnd_level': 1029.31,
                                    'humidity': 69,
                                    'pressure': 1029.31,
                                    'sea_level': 1033.14,
                                    'temp': 293.867,
                                    'temp_kf': 0,
                                    'temp_max': 293.867,
                                    'temp_min': 293.867},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'broken clouds',
                                           'icon': '04d',
                                           'id': 803,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 195.003, 'speed': 5.42}},
                    {   'clouds': {'all': 8},
                        'dt': 1525057200,
                        'dt_txt': '2018-04-30 03:00:00',
                        'main': {   'grnd_level': 1028.32,
                                    'humidity': 65,
                                    'pressure': 1028.32,
                                    'sea_level': 1032.01,
                                    'temp': 294.983,
                                    'temp_kf': 0,
                                    'temp_max': 294.983,
                                    'temp_min': 294.983},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '02d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 190.001, 'speed': 6.45}},
                    {   'clouds': {'all': 32},
                        'dt': 1525068000,
                        'dt_txt': '2018-04-30 06:00:00',
                        'main': {   'grnd_level': 1026.99,
                                    'humidity': 67,
                                    'pressure': 1026.99,
                                    'sea_level': 1030.66,
                                    'temp': 294.331,
                                    'temp_kf': 0,
                                    'temp_max': 294.331,
                                    'temp_min': 294.331},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'scattered clouds',
                                           'icon': '03d',
                                           'id': 802,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 188.506, 'speed': 6.28}},
                    {   'clouds': {'all': 92},
                        'dt': 1525078800,
                        'dt_txt': '2018-04-30 09:00:00',
                        'main': {   'grnd_level': 1026.47,
                                    'humidity': 76,
                                    'pressure': 1026.47,
                                    'sea_level': 1030.14,
                                    'temp': 292.533,
                                    'temp_kf': 0,
                                    'temp_max': 292.533,
                                    'temp_min': 292.533},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'overcast clouds',
                                           'icon': '04d',
                                           'id': 804,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 183.003, 'speed': 5.39}},
                    {   'clouds': {'all': 12},
                        'dt': 1525089600,
                        'dt_txt': '2018-04-30 12:00:00',
                        'main': {   'grnd_level': 1027.19,
                                    'humidity': 85,
                                    'pressure': 1027.19,
                                    'sea_level': 1030.97,
                                    'temp': 291.324,
                                    'temp_kf': 0,
                                    'temp_max': 291.324,
                                    'temp_min': 291.324},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'few clouds',
                                           'icon': '02n',
                                           'id': 801,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 192.504, 'speed': 4.84}},
                    {   'clouds': {'all': 0},
                        'dt': 1525100400,
                        'dt_txt': '2018-04-30 15:00:00',
                        'main': {   'grnd_level': 1026.65,
                                    'humidity': 94,
                                    'pressure': 1026.65,
                                    'sea_level': 1030.52,
                                    'temp': 290.028,
                                    'temp_kf': 0,
                                    'temp_max': 290.028,
                                    'temp_min': 290.028},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01n',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 202.002, 'speed': 3.52}},
                    {   'clouds': {'all': 0},
                        'dt': 1525111200,
                        'dt_txt': '2018-04-30 18:00:00',
                        'main': {   'grnd_level': 1026.43,
                                    'humidity': 95,
                                    'pressure': 1026.43,
                                    'sea_level': 1030.38,
                                    'temp': 288.078,
                                    'temp_kf': 0,
                                    'temp_max': 288.078,
                                    'temp_min': 288.078},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01n',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 215.5, 'speed': 0.95}},
                    {   'clouds': {'all': 0},
                        'dt': 1525122000,
                        'dt_txt': '2018-04-30 21:00:00',
                        'main': {   'grnd_level': 1027.48,
                                    'humidity': 93,
                                    'pressure': 1027.48,
                                    'sea_level': 1031.36,
                                    'temp': 288.515,
                                    'temp_kf': 0,
                                    'temp_max': 288.515,
                                    'temp_min': 288.515},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 347.004, 'speed': 1.39}},
                    {   'clouds': {'all': 24},
                        'dt': 1525132800,
                        'dt_txt': '2018-05-01 00:00:00',
                        'main': {   'grnd_level': 1028.05,
                                    'humidity': 78,
                                    'pressure': 1028.05,
                                    'sea_level': 1031.84,
                                    'temp': 293.433,
                                    'temp_kf': 0,
                                    'temp_max': 293.433,
                                    'temp_min': 293.433},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'few clouds',
                                           'icon': '02d',
                                           'id': 801,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 354.002, 'speed': 2}},
                    {   'clouds': {'all': 0},
                        'dt': 1525143600,
                        'dt_txt': '2018-05-01 03:00:00',
                        'main': {   'grnd_level': 1027.23,
                                    'humidity': 68,
                                    'pressure': 1027.23,
                                    'sea_level': 1030.97,
                                    'temp': 295.814,
                                    'temp_kf': 0,
                                    'temp_max': 295.814,
                                    'temp_min': 295.814},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'clear sky',
                                           'icon': '01d',
                                           'id': 800,
                                           'main': 'Clear'}],
                        'wind': {'deg': 58.0005, 'speed': 1.95}},
                    {   'clouds': {'all': 12},
                        'dt': 1525154400,
                        'dt_txt': '2018-05-01 06:00:00',
                        'main': {   'grnd_level': 1025.78,
                                    'humidity': 59,
                                    'pressure': 1025.78,
                                    'sea_level': 1029.67,
                                    'temp': 296.655,
                                    'temp_kf': 0,
                                    'temp_max': 296.655,
                                    'temp_min': 296.655},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'few clouds',
                                           'icon': '02d',
                                           'id': 801,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 100.501, 'speed': 2.42}},
                    {   'clouds': {'all': 12},
                        'dt': 1525165200,
                        'dt_txt': '2018-05-01 09:00:00',
                        'main': {   'grnd_level': 1027.03,
                                    'humidity': 59,
                                    'pressure': 1027.03,
                                    'sea_level': 1030.85,
                                    'temp': 294.82,
                                    'temp_kf': 0,
                                    'temp_max': 294.82,
                                    'temp_min': 294.82},
                        'rain': {},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'few clouds',
                                           'icon': '02d',
                                           'id': 801,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 132, 'speed': 2.27}},
                    {   'clouds': {'all': 44},
                        'dt': 1525176000,
                        'dt_txt': '2018-05-01 12:00:00',
                        'main': {   'grnd_level': 1029.06,
                                    'humidity': 84,
                                    'pressure': 1029.06,
                                    'sea_level': 1032.88,
                                    'temp': 290.977,
                                    'temp_kf': 0,
                                    'temp_max': 290.977,
                                    'temp_min': 290.977},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'scattered clouds',
                                           'icon': '03n',
                                           'id': 802,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 130.5, 'speed': 2.14}},
                    {   'clouds': {'all': 92},
                        'dt': 1525186800,
                        'dt_txt': '2018-05-01 15:00:00',
                        'main': {   'grnd_level': 1029.44,
                                    'humidity': 95,
                                    'pressure': 1029.44,
                                    'sea_level': 1033.24,
                                    'temp': 289.818,
                                    'temp_kf': 0,
                                    'temp_max': 289.818,
                                    'temp_min': 289.818},
                        'rain': {},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'overcast clouds',
                                           'icon': '04n',
                                           'id': 804,
                                           'main': 'Clouds'}],
                        'wind': {'deg': 68.5019, 'speed': 2.82}},
                    {   'clouds': {'all': 88},
                        'dt': 1525197600,
                        'dt_txt': '2018-05-01 18:00:00',
                        'main': {   'grnd_level': 1029.78,
                                    'humidity': 93,
                                    'pressure': 1029.78,
                                    'sea_level': 1033.54,
                                    'temp': 289.925,
                                    'temp_kf': 0,
                                    'temp_max': 289.925,
                                    'temp_min': 289.925},
                        'rain': {'3h': 0.08025},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10n',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 54.0002, 'speed': 3.87}},
                    {   'clouds': {'all': 80},
                        'dt': 1525208400,
                        'dt_txt': '2018-05-01 21:00:00',
                        'main': {   'grnd_level': 1030.19,
                                    'humidity': 89,
                                    'pressure': 1030.19,
                                    'sea_level': 1033.89,
                                    'temp': 289.47,
                                    'temp_kf': 0,
                                    'temp_max': 289.47,
                                    'temp_min': 289.47},
                        'rain': {'3h': 0.0454},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10d',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 57.5014, 'speed': 4.71}},
                    {   'clouds': {'all': 76},
                        'dt': 1525219200,
                        'dt_txt': '2018-05-02 00:00:00',
                        'main': {   'grnd_level': 1030.5,
                                    'humidity': 77,
                                    'pressure': 1030.5,
                                    'sea_level': 1034.33,
                                    'temp': 291.644,
                                    'temp_kf': 0,
                                    'temp_max': 291.644,
                                    'temp_min': 291.644},
                        'rain': {'3h': 0.00755},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10d',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 49.0068, 'speed': 3.66}},
                    {   'clouds': {'all': 92},
                        'dt': 1525230000,
                        'dt_txt': '2018-05-02 03:00:00',
                        'main': {   'grnd_level': 1029.66,
                                    'humidity': 85,
                                    'pressure': 1029.66,
                                    'sea_level': 1033.34,
                                    'temp': 291.125,
                                    'temp_kf': 0,
                                    'temp_max': 291.125,
                                    'temp_min': 291.125},
                        'rain': {'3h': 0.59005},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10d',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 65.5038, 'speed': 3.37}},
                    {   'clouds': {'all': 92},
                        'dt': 1525240800,
                        'dt_txt': '2018-05-02 06:00:00',
                        'main': {   'grnd_level': 1027.91,
                                    'humidity': 95,
                                    'pressure': 1027.91,
                                    'sea_level': 1031.6,
                                    'temp': 290.306,
                                    'temp_kf': 0,
                                    'temp_max': 290.306,
                                    'temp_min': 290.306},
                        'rain': {'3h': 0.671},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10d',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 51.001, 'speed': 2.85}},
                    {   'clouds': {'all': 100},
                        'dt': 1525251600,
                        'dt_txt': '2018-05-02 09:00:00',
                        'main': {   'grnd_level': 1026.1,
                                    'humidity': 100,
                                    'pressure': 1026.1,
                                    'sea_level': 1029.88,
                                    'temp': 289.543,
                                    'temp_kf': 0,
                                    'temp_max': 289.543,
                                    'temp_min': 289.543},
                        'rain': {'3h': 2.46165},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10d',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 38.5005, 'speed': 2.42}},
                    {   'clouds': {'all': 92},
                        'dt': 1525262400,
                        'dt_txt': '2018-05-02 12:00:00',
                        'main': {   'grnd_level': 1025.24,
                                    'humidity': 100,
                                    'pressure': 1025.24,
                                    'sea_level': 1028.99,
                                    'temp': 289.284,
                                    'temp_kf': 0,
                                    'temp_max': 289.284,
                                    'temp_min': 289.284},
                        'rain': {'3h': 1.01165},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10n',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 351.503, 'speed': 1.86}},
                    {   'clouds': {'all': 92},
                        'dt': 1525273200,
                        'dt_txt': '2018-05-02 15:00:00',
                        'main': {   'grnd_level': 1022.24,
                                    'humidity': 100,
                                    'pressure': 1022.24,
                                    'sea_level': 1026.06,
                                    'temp': 289.129,
                                    'temp_kf': 0,
                                    'temp_max': 289.129,
                                    'temp_min': 289.129},
                        'rain': {'3h': 2.24495},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'light rain',
                                           'icon': '10n',
                                           'id': 500,
                                           'main': 'Rain'}],
                        'wind': {'deg': 184.503, 'speed': 0.73}},
                    {   'clouds': {'all': 92},
                        'dt': 1525284000,
                        'dt_txt': '2018-05-02 18:00:00',
                        'main': {   'grnd_level': 1018.63,
                                    'humidity': 100,
                                    'pressure': 1018.63,
                                    'sea_level': 1022.42,
                                    'temp': 289.558,
                                    'temp_kf': 0,
                                    'temp_max': 289.558,
                                    'temp_min': 289.558},
                        'rain': {'3h': 4.4076},
                        'sys': {'pod': 'n'},
                        'weather': [   {   'description': 'moderate rain',
                                           'icon': '10n',
                                           'id': 501,
                                           'main': 'Rain'}],
                        'wind': {'deg': 302.501, 'speed': 1.31}},
                    {   'clouds': {'all': 100},
                        'dt': 1525294800,
                        'dt_txt': '2018-05-02 21:00:00',
                        'main': {   'grnd_level': 1016.53,
                                    'humidity': 100,
                                    'pressure': 1016.53,
                                    'sea_level': 1020.45,
                                    'temp': 290.15,
                                    'temp_kf': 0,
                                    'temp_max': 290.15,
                                    'temp_min': 290.15},
                        'rain': {'3h': 4.3725},
                        'sys': {'pod': 'd'},
                        'weather': [   {   'description': 'moderate rain',
                                           'icon': '10d',
                                           'id': 501,
                                           'main': 'Rain'}],
                        'wind': {'deg': 229.501, 'speed': 1.88}}],
        'message': 0.0111}
    

## 気温だけを表示


```python
# 今までのプログラムに以下を追記
w_list = f_dict["list"]
for w_dict in w_list:
    print(w_dict["main"]["temp"])
```

    296.29
    296.75
    295.63
    293.03
    289.808
    289.786
    289.608
    290.277
    293.94
    294.825
    294.837
    293.168
    291.804
    291.31
    290.972
    290.96
    293.867
    294.983
    294.331
    292.533
    291.324
    290.028
    288.078
    288.515
    293.433
    295.814
    296.655
    294.82
    290.977
    289.818
    289.925
    289.47
    291.644
    291.125
    290.306
    289.543
    289.284
    289.129
    289.558
    290.15
    

## 課題3-3
時刻、温度、天気、風の強さの予報を、ダブルクオートで括って、カンマ区切りで表示せよ。

期待する出力

```
"2018-04-28 09:00:00+09:00","23.140000000000043","Clear","1.81"
"2018-04-28 12:00:00+09:00","23.600000000000023","Clouds","0.22"
"2018-04-28 15:00:00+09:00","22.480000000000018","Rain","4.57"
"2018-04-28 18:00:00+09:00","19.879999999999995","Clouds","4.65"
"2018-04-28 21:00:00+09:00","16.658000000000015","Clear","4.71"
"2018-04-29 00:00:00+09:00","16.636000000000024","Clear","4.56"
"2018-04-29 03:00:00+09:00","16.458000000000027","Clear","4.67"
"2018-04-29 06:00:00+09:00","17.12700000000001","Clear","3.76"
"2018-04-29 09:00:00+09:00","20.79000000000002","Rain","4.46"
"2018-04-29 12:00:00+09:00","21.67500000000001","Clear","6.77"
"2018-04-29 15:00:00+09:00","21.687000000000012","Clear","7.52"
"2018-04-29 18:00:00+09:00","20.01800000000003","Clear","7.36"
"2018-04-29 21:00:00+09:00","18.653999999999996","Clear","6.61"
"2018-04-30 00:00:00+09:00","18.160000000000025","Clouds","5.81"
"2018-04-30 03:00:00+09:00","17.822000000000003","Clear","5.16"
"2018-04-30 06:00:00+09:00","17.810000000000002","Clouds","4.91"
"2018-04-30 09:00:00+09:00","20.71700000000004","Clouds","5.42"
"2018-04-30 12:00:00+09:00","21.833000000000027","Clear","6.45"
"2018-04-30 15:00:00+09:00","21.18100000000004","Clouds","6.28"
"2018-04-30 18:00:00+09:00","19.383000000000038","Clouds","5.39"
```

ヒント：ダブルクオート "  をprintしたいときは、文字列をシングルクオート ' で定義する。   print('ここは"大阪"です')
