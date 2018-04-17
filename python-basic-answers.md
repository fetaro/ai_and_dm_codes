
# 演習の答え

## 演習1-1答え


```python
print("2の30乗は{0}です".format(2**30))   
```

    2の30乗は1073741824です


## 演習1-2答え


```python
sum = 0
for i in range(1,11):
    sum += i**2
print(sum)    
```

    385


## 演習1-3の答え


```python
for i in range(1,51):
    if(i%3 == 0):
        print("{0} is multiples of 3".format(i))
    else:
        print(i)
```

    1
    2
    3 is multiples of 3
    4
    5
    6 is multiples of 3
    7
    8
    9 is multiples of 3
    10
    11
    12 is multiples of 3
    13
    14
    15 is multiples of 3
    16
    17
    18 is multiples of 3
    19
    20
    21 is multiples of 3
    22
    23
    24 is multiples of 3
    25
    26
    27 is multiples of 3
    28
    29
    30 is multiples of 3
    31
    32
    33 is multiples of 3
    34
    35
    36 is multiples of 3
    37
    38
    39 is multiples of 3
    40
    41
    42 is multiples of 3
    43
    44
    45 is multiples of 3
    46
    47
    48 is multiples of 3
    49
    50


## 演習1-4の答え


```python
def fibo(n):
    if(n == 0):
        return 0
    elif(n == 1):
        return 1
    else:
        return fibo(n-2) + fibo(n-1)
    
print(fibo(20))
```

    6765


## 演習1-5の答え


```python
filename = "sample.txt"
with open(filename, "r") as file: 
    for index,line in enumerate(file.readlines()):
        print("{0}行目:{1}".format(index,line))
```

    0行目:apple
    
    1行目:orange
    
    2行目:banana


## 演習1-6の答え


```python
# -*- coding: utf-8 -*-
def delete_both_ends(str):
    tmp = str[:-1]
    return tmp[1:]

filename = "13TOKYO.CSV"
with open(filename, "r", encoding='shift_jis') as file: 
    for index,line in enumerate(file.readlines()):
        tokens = line.split(",")
        print("郵便番号:{0}, 旧郵便番号:{1}".format(
            delete_both_ends(tokens[2]),
            delete_both_ends(tokens[1])
        ))
        if(index >= 9):
            break #10行を超えたらループを抜ける
```

    郵便番号:1000000, 旧郵便番号:100  
    郵便番号:1020072, 旧郵便番号:102  
    郵便番号:1020082, 旧郵便番号:102  
    郵便番号:1010032, 旧郵便番号:101  
    郵便番号:1010047, 旧郵便番号:101  
    郵便番号:1000011, 旧郵便番号:100  
    郵便番号:1000004, 旧郵便番号:100  
    郵便番号:1006890, 旧郵便番号:100  
    郵便番号:1006801, 旧郵便番号:100  
    郵便番号:1006802, 旧郵便番号:100  


## 演習1-7の答え


```python
def delete_both_ends(str):
    tmp = str[:-1]
    return tmp[1:]

filename = "13TOKYO.CSV"

def lookup_kanji_address(address):
    with open(filename, "r",encoding='shift_jis') as file: 
        for index,line in enumerate(file.readlines()):
            tokens = line.split(",")
            if( address  == delete_both_ends(tokens[2])):
                print("{0}　{1}　{2}".format(delete_both_ends(tokens[6]),delete_both_ends(tokens[7]),delete_both_ends(tokens[8])))
                
lookup_kanji_address("1420043")
```

    東京都　品川区　二葉

