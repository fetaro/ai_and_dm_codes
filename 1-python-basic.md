
# Pythonの基礎

## 印字


```python
print("hello world")
```

    hello world
    

## 四則演算


```python
print(1 + 1)
```

    2
    


```python
print((1 + 2 * 4 -3) / 5)
```

    1.2
    


```python
print(2 ** 8)
```

    256
    

## 変数


```python
x = 1
y = 1 / 3
print(x + y)
```

    1.3333333333333333
    

## 演算して代入


```python
x = 1
print(x)
x += 3
print(x)
```

    1
    4
    

## 型
|型|名前|例|
|------|----------|-------|
| int | 整数(32bit)| a = 1 |
| float | 浮動小数点数(32bit)| a = 1.5 |
| str |  文字列 | a = "abc" |
| bool | 真偽値 | a = True |
| list | 配列  |a = [1,2,3] |
| dict | ディクショナリ | a = { "k1" : "v1" } |


型を調べる


```python
print(type(1.5))
```

    <class 'float'>
    

## 文字列


```python
print('abc')
```

    abc
    


```python
print('abc')
```

    abc
    


```python
print('abc' + 'def')
```

    abcdef
    

## 配列


```python
a = [2,4,6]
print(a[0])
print(a[1])
print(a[2])
```

    2
    4
    6
    


```python
print(a)
```

    [2, 4, 6]
    


```python
# 存在しない要素にアクセスした場合
print(a[3])
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-14-5451d47c444b> in <module>()
    ----> 1 print(a[3])
    

    IndexError: list index out of range


配列の要素の置換


```python
a[1] = 8
print(a)
```

配列の長さ


```python
print(len(a))
```

    3
    

## 連続した要素


```python
y = range(5)
print(y[0])
print(y[1])
print(y[2])
print(y[3])
print(y[4])
```

    0
    1
    2
    3
    4
    


```python
y = range(6,11)
print(y[0])
print(y[1])
print(y[2])
print(y[3])
print(y[4])
```

    6
    7
    8
    9
    10
    

## ディクショナリ


```python
colors = {"carrot":"orange", "tomato": "red", "corn":"yellow" }
print(colors)
```

    {'carrot': 'orange', 'tomato': 'red', 'corn': 'yellow'}
    


```python
print(colors["tomato"])
```

    red
    


```python
colors["cucumber"] = "green"
print(colors)
```

    {'carrot': 'orange', 'tomato': 'red', 'corn': 'yellow', 'cucumber': 'green'}
    

## 真偽値


```python
a = True
print(a)
b = False
print(b)
```

    True
    False
    


```python
c = 10 > 11
print(c)
```

    False
    


```python
d = ("abc" == "abd")
print(d)
```

    False
    

## 比較演算子


```python
a == b
a >  b
a >= b
a <  b
a <= b
a != b
```




    True



## 制御構造

## if文


```python
x = 11
if x > 10:
    print("x is larger than 10")
else:
    print("x is smaller than 11")
```

    x is larger than 10
    

文法

```
if 真偽値 :　(←セミコロン)
    実行したい文
```

セミコロンの後は、インデント（字下げ）としてタブまたは半角スペース4つが必要

## for文


```python
for i in [1,2,3]:
    print(i)
```

    1
    2
    3
    

文法

```
for 変数 in list型 :
    実行したい文
```


```python
for i in range(5,9):
    print(i)
```

    5
    6
    7
    8
    

配列のindexと要素を同時に取得する


```python
for index,element in enumerate([3,6,9,12]):
    print(index)
    print(element)
```

    0
    3
    1
    6
    2
    9
    3
    12
    

ループを途中で抜ける時は `break`を使う


```python
for i in range(0,9):
    print(i)
    if(i == 3):
        break
```

    0
    1
    2
    3
    

そのあとの処理をせずに次のループに入る場合は `continue` を使う


```python
for i in range(0,9):
    print(i)
    if(i > 3):
        continue
    print("a")
```

    0
    a
    1
    a
    2
    a
    3
    a
    4
    5
    6
    7
    8
    

## 関数


```python
def f(a, b):
    y =  3 * a + 5 * b
    return y


print( f(10,5) )

# 引数の名前を指定する事もできる
print( f(a=1, b=3) )
```

    55
    18
    

## 文字列のフォーマッティング

format()関数

(文字列).format( {0}に代入する値, {1}に代入する値, ・・・ )


```python
x =4
y = 3.5
str = "the value of x is {0} , and y is {1}.".format(x,y)
print(str)
```

    the value of x is 4 , and y is 3.5.
    


```python
name = "watanabe"
age = 35
str = "Mr.{0} is {1} years old".format(name,age)
print(str)
```

    Mr.watanabe is 35 years old
    

## コメント


```python
#　一行コメントは

'''
複数行
コメント
'''

```




    '\n複数行\nコメント\n'



## 演習1-1
２の３０乗を計算し `2の30乗は○○です` と印字せよ

## 演習1-2
１～１０までの整数の各値の２乗の和をprintせよ   つまり `1 + 4 + 9 + 16 ・・・ 2500` の結果をプリントせよ

## 演習1-3
１～５０までの数字を印字しながら、3の倍数の時だけ、"N is multiples of 3"　と印字せよ
　　出力例
    　　1
        2
        3 is multiples of 3
        4
        5
        6 is multiples of 3
        7
   
    ヒント
        割った余りを計算するときには % 演算子を使う   7 % 3 → 1
## 演習1-4 

フィボナッチ数列の第20項を求めよ

フィボナッチ数列
   第0項 = 0,
   第1項 = 1,
   第n+2項 = 第n+0項 + 第n+1項
