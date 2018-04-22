
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
    
