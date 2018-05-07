
# 演習の答え

## 演習2-1の答え


```python
filename = "sample.txt"
with open(filename, "r") as file: 
    for index,line in enumerate(file.readlines()):
        print("{0}行目:{1}".format(index,line))
```

    0行目:apple
    
    1行目:orange
    
    2行目:banana
    

## 演習2-2の答え


```python
# -*- coding: utf-8 -*-

# 文字列の両端の文字を消す
def del_ends(str):
    tmp = str[:-1]
    return tmp[1:]

filename = "13TOKYO.CSV"
with open(filename, "r", encoding='shift_jis') as file: 
    for index,line in enumerate(file.readlines()):
        tokens = line.split(",")
        print("郵便番号:{0}, 旧郵便番号:{1}".format(
            del_ends(tokens[2]),
            del_ends(tokens[1])
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
    

## 演習2-3の答え


```python
# -*- coding: utf-8 -*-

# Delete both ends
def del_ends(str):
    tmp = str[:-1]
    return tmp[1:]

filename = "13TOKYO.CSV"

def lookup_kanji_address(address):
    with open(filename, "r",encoding='shift_jis') as file: 
        for index,line in enumerate(file.readlines()):
            tokens = line.split(",")
            if( address  == del_ends(tokens[2])):
                print("{0}　{1}　{2}".format(del_ends(tokens[6]),del_ends(tokens[7]),del_ends(tokens[8])))
                
lookup_kanji_address("1420043")
lookup_kanji_address("1420042")
```

    東京都　品川区　二葉
    東京都　品川区　豊町
    

## 演習2-4の答え


```python
# -*- coding: utf-8 -*-

# 文字列の両端の文字を消す
def del_ends(str):
    tmp = str[:-1]
    return tmp[1:]

filename = "13TOKYO.CSV"

address_dict = {}

with open(filename, "r",encoding='shift_jis') as file: 
    for index,line in enumerate(file.readlines()):
        tokens = line.split(",")
        address = del_ends(tokens[2])
        address_dict[address] = "{0}　{1}　{2}".format(del_ends(tokens[6]),del_ends(tokens[7]),del_ends(tokens[8]))
                
def lookup_kanji_address(address):
    return address_dict[address]
                
print(lookup_kanji_address("1420043"))
print(lookup_kanji_address("1420042"))
```

    東京都　品川区　二葉
    東京都　品川区　豊町
    

## 演習2-5の答え


```python
# -*- coding: utf-8 -*-

# 文字列の両端の文字を消す
def del_ends(str):
    tmp = str[:-1]
    return tmp[1:]

filename_list = ["13TOKYO.CSV","11SAITAM.CSV","14KANAGA.CSV"]

address_dict = {}
for filename in filename_list:
    with open(filename, "r",encoding='shift_jis') as file: 
        for index,line in enumerate(file.readlines()):
            tokens = line.split(",")
            address = del_ends(tokens[2])
            address_dict[address] = "{0}　{1}　{2}".format(del_ends(tokens[6]),del_ends(tokens[7]),del_ends(tokens[8]))
                
def lookup_kanji_address(address):
    return address_dict[address]
                
print(lookup_kanji_address("3380012"))
print(lookup_kanji_address("2210821"))
```

    埼玉県　さいたま市中央区　大戸
    神奈川県　横浜市神奈川区　富家町
    


```python
# -*- coding: utf-8 -*-

input_filename = "13TOKYO.CSV"
output_filename = "13TOKYO-FILTERD.CSV"
with open(output_filename,"w", encoding='shift_jis') as output_file:
    with open(input_filename, "r", encoding='shift_jis') as input_file: 
        for line in input_file.readlines():
            tokens = line.split(",")
            output_file.write("{0},{1}\n".format(tokens[2],tokens[1]))

```
