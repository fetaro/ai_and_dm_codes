
# PythonからMySQLにデータを挿入する

### まずやってみよう

以下のコードを書いて実行

```python
import mysql.connector
```

すると以下の様にエラーになる。これはPythonからMySQLに接続するためのライブラリがないため。

```
ModuleNotFoundError: No module named 'mysql'
```

そこで Python-MySQLドライバのインストールをする必要がある

### Python-MySQLドライバのインストール

1. Anaconda Navigatorを起動→左のタブからEnvironmentsを選択 → この画面でインストールしているライブラリの一覧を見ることができる

2. InstalledとなっているプルダウンをAllに変更し、 Search Packagesの欄に「MySQL」と入力する → これによりまだインストールしていないライブラリの中からMySQLという文字が含まれるライブラリを検索している

3. mysql-connector-python　を選択して、Applyをクリック

![5-1.png](5-1.png)

4. install packagesで以下の画面になった準備完了。Applyをクリック

<img src="5-2.png" width="200">

5. spyderに戻り`import mysql.connector`が書かれたプログラムを実行し、エラーが出なければOK

※)以下の様な画面が出た場合は、「Anaconda Navigatorを最新にバージョンアップをしないか？」といってきているので、Noを選択すればOK

<img src="5-3.png" width="200">
