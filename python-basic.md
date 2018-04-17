
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
１～１０までの整数の各値の２乗の和をprintせよ   つまり `1 + 4 + 9 + 16 ・・・ + 100` の結果をプリントせよ

## 演習1-3
１～５０までの数字を印字しながら、3の倍数の時だけ、"N is multiples of 3"　と印字せよ
```
　　出力例
    　   　1
        2
        3 is multiples of 3
        4
        5
        6 is multiples of 3
        7
```
    ヒント
        割った余りを計算するときには % 演算子を使う   7 % 3 → 1
## 演習1-4 

フィボナッチ数列の第20項を求めよ

フィボナッチ数列
   第0項 = 0
   第1項 = 1
   第n+2項 = 第n+1項 + 第n+2項

## ソースコードの文字コード指定

一行目にある

```
# -*- coding: utf-8 -*-
```

はこのソースコードではutf-8の文字コードで日本語を扱うことをpythonに教える役割がある。これが無いと日本語を含むソースコードは動作しない。

## ファイル入力の準備

ディレクトリの中に2つのファイルを用意

```
(好きなディレクトリ)
  ├ load_file.py
  └ sample.txt
```


sample.txtの中身
```
apple
orange
banana
```

load_file.pyの中身は空でOK

## ファイルの入力

spyderでload_file.pyを開く


```python
# ファイルのクローズを明示する書き方（レガシー）

filename = "sample.txt"      #ファイル名を変数に格納
file = open(filename, "r")    # "r"はファイル読み込み専用
str = file.read()             #ファイル全体を読み込む
print(str)
file.close()                  #ファイルを閉じる
```

    apple
    orange
    banana



```python
# with句を用いるやり方（推奨）

filename = "sample.txt"
with open(filename, "r") as file:  #ファイルを開いてfileという変数に格納
    str = file.read()
    print(str)
    
    # このブロックを抜けると自動的にcloseしてくれる。closeし忘れを回避できる
```

    apple
    orange
    banana



```python
# ファイルを一行ずつ読む関数

filename = "sample.txt"
with open(filename, "r") as file: 
    for line in file.readlines():
        print(line)

```

    apple
    
    orange
    
    banana


## 演習1-5
以下のファイルの各行の先頭に"n行目:"という文字列を付けて表示せよ

1行目:apple
2行目:orange
3行目:banana

ヒント　enumerate()
## pythonのドキュメントを読む

pythonのドキュメント
* https://docs.python.jp/3/index.html

open()のドキュメント
* https://docs.python.jp/3/library/functions.html?highlight=open#open
* https://docs.python.jp/3/tutorial/inputoutput.html#index-0
    

## CSVファイルを読み込む

ファイル入出力の事前作業として、入力するファイルとソースコードを同じディレクトリに配置しておく

1. 東京の郵便番号CSVをダウンロード  http://www.post.japanpost.jp/zipcode/dl/oogaki-zip.html
2. 13TOKYO.CSVを作業ディレクトリに置く
3. 同じディレクトリに load_csv.py という名前で空ファイルを作る
4. spyderから　ファイル→開く→load_csv.pyを選択しそこにソースコードを書く


```python
filename = "13TOKYO.CSV"
with open(filename, "r", encoding='shift_jis') as file: # CSVに日本語が含まれて、Shift-JISであるためエンコーディングの指定が必要
    for index,line in enumerate(file.readlines()):
        print(line)
        if(index > 10):
            break #10行を超えたらループを抜ける
```

    13101,"100  ","1000000","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｲｶﾆｹｲｻｲｶﾞﾅｲﾊﾞｱｲ","東京都","千代田区","以下に掲載がない場合",0,0,0,0,0,0
    
    13101,"102  ","1020072","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｲｲﾀﾞﾊﾞｼ","東京都","千代田区","飯田橋",0,0,1,0,0,0
    
    13101,"102  ","1020082","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｲﾁﾊﾞﾝﾁﾖｳ","東京都","千代田区","一番町",0,0,0,0,0,0
    
    13101,"101  ","1010032","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｲﾜﾓﾄﾁﾖｳ","東京都","千代田区","岩本町",0,0,1,0,0,0
    
    13101,"101  ","1010047","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｳﾁｶﾝﾀﾞ","東京都","千代田区","内神田",0,0,1,0,0,0
    
    13101,"100  ","1000011","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｳﾁｻｲﾜｲﾁﾖｳ","東京都","千代田区","内幸町",0,0,1,0,0,0
    
    13101,"100  ","1000004","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｵｵﾃﾏﾁ(ﾂｷﾞﾉﾋﾞﾙｦﾉｿﾞｸ)","東京都","千代田区","大手町（次のビルを除く）",0,0,1,0,0,0
    
    13101,"100  ","1006890","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｵｵﾃﾏﾁｼﾞｴｲｴｲﾋﾞﾙ(ﾁｶｲ･ｶｲｿｳﾌﾒｲ)","東京都","千代田区","大手町ＪＡビル（地階・階層不明）",0,0,0,0,0,0
    
    13101,"100  ","1006801","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｵｵﾃﾏﾁｼﾞｴｲｴｲﾋﾞﾙ(1ｶｲ)","東京都","千代田区","大手町ＪＡビル（１階）",0,0,0,0,0,0
    
    13101,"100  ","1006802","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｵｵﾃﾏﾁｼﾞｴｲｴｲﾋﾞﾙ(2ｶｲ)","東京都","千代田区","大手町ＪＡビル（２階）",0,0,0,0,0,0
    
    13101,"100  ","1006803","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｵｵﾃﾏﾁｼﾞｴｲｴｲﾋﾞﾙ(3ｶｲ)","東京都","千代田区","大手町ＪＡビル（３階）",0,0,0,0,0,0
    
    13101,"100  ","1006804","ﾄｳｷﾖｳﾄ","ﾁﾖﾀﾞｸ","ｵｵﾃﾏﾁｼﾞｴｲｴｲﾋﾞﾙ(4ｶｲ)","東京都","千代田区","大手町ＪＡビル（４階）",0,0,0,0,0,0
    


## 文字列の分割(split)


```python
str = "123,hoge,渡部"

tokens = str.split(",")

print(tokens)
print(tokens[0])
print(tokens[1])
print(tokens[2])
```

    ['123', 'hoge', '渡部']
    123
    hoge
    渡部


## 部分文字列の取得


```python
str = "abcdefg"
print(str[:2]) #2文字目以前
print(str[2:]) #2文字目より後ろ
print(str[3:5]) #3文字目より後ろで、5文字目以前
print(str[:-1]) #後ろから1文字
```

    ab
    cdefg
    de
    abcdef


## CSVの2列目だけを表示


```python
filename = "13TOKYO.CSV"
with open(filename, "r", encoding='shift_jis') as file: 
    for index,line in enumerate(file.readlines()):
        tokens = line.split(",")
        print(tokens[2])
        if(index >= 9):
            break #10行を超えたらループを抜ける
```

    "1000000"
    "1020072"
    "1020082"
    "1010032"
    "1010047"
    "1000011"
    "1000004"
    "1006890"
    "1006801"
    "1006802"


## 演習1-6

東京の郵便番号CSV「13TOKYO.CSV」から 郵便番号と旧郵便番号を10行表示せよ

表示

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
```

ヒント：郵便番号と旧郵便番号が何列目にあるかは　→　http://www.post.japanpost.jp/zipcode/dl/readme.html
ヒント：","でsplitするだけだと両端にダブルクオートが残ってしまう。ダブルクオートを削除するためには、部分文字列を取得する
    

## 演習 1-7

郵便番号を第一引数として、入力して都道府県名 市区町村名 町域名　を全角スペースで連結した文字列を返却する関数 lookup_kanji_address() 関数を作成せよ

```
print(lookup_kanji_address('1020072'))

=> "東京都　千代田区　飯田橋"
```

ヒント：ダブルクオートを文字列に含めたい場合はシングルクオートで文字を定義する '"'

## 演習 1-8 (余裕がある人は)

* 関数を呼び出すたびにCSVファイルを開かなくても答えを返せるようにせよ
* 東京、神奈川、埼玉の3つのファイルから検索できるようにせよ
