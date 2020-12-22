# Pythonの基礎

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [tuple (タプル)](#tuple-タプル)
    - [tupleとListの違い](#tupleとlistの違い)
- [tupleの使い方](#tupleの使い方)
    - [要素の追加](#要素の追加)
    - [要素の削除](#要素の削除)
    - [要素の変更](#要素の変更)
    - [taple同士の比較](#taple同士の比較)
    - [tapleの検索](#tapleの検索)
- [Python標準のリストとNumPyの配列（NumPy.ndarray）の使い分け](#python標準のリストとnumpyの配列numpyndarrayの使い分け)
- [Python標準のリストは異なる型を格納できる？](#python標準のリストは異なる型を格納できる)
- [エラーが出たら](#エラーが出たら)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## tuple (タプル)
タプルとは、データ構造の一つでリストと同じように複数の値を持つことができる。

### tupleとListの違い

また、リストとタプルにはこのような違いがあります。

- イミュータブル（変更ができない）
- 実行速度が少し早い

リストには要素を追加したり、要素を消したりすることもできますが、**タプルではできません。**

```
# リスト
list_sample = [1, 2, 3, 4, 5]

# タプル
tuple_sample = (1, 2, 3, 4, 5)
```
※タプルは（）で囲わなくても問題ないけど、区別するために（）で囲んだほうがわかりやすい。

## tupleの使い方

### 要素の追加

タプルはイミュータブルなので一度作ると変更ができない。

でも**別のタプルを作って連結をすること**で、要素の追加のような振る舞いにすることはできる。

```
tuple_sample1 = (1, 2, 3, 4, 5)
tuple_sample2 = tuple_sample1 + (6, 7)

print(tuple_sample2)
```

実行結果
```
(1, 2, 3, 4, 5, 6, 7)
```

### 要素の削除
タプルは変更ができないので**要素を削除する事もできない。**

ですが、「スライス」という機能を使って**部分的に取り出したタプルを作ることはできる。**

```
tuple_sample1 = (1, 2, 3, 4, 5)
tuple_sample2 = tuple_sample1[2:4:1]

print(tuple_sample2)
```
実行結果
```
(3, 4)
```

tuple_sample1のタプルから、インデックス2（3番目）からインデックス4（4番目まで）を1つずつ（1ステップずつ）、抜き出してtuple_sample2を作りました。

※Pythonはインデックスが0スタート

### 要素の変更
**要素の変更はできない。**


リストと同じように変更しようとすると・・・
```
tuple_sample = (1, 2, 3, 4, 5)
tuple_sample[2] = 10
```

実行結果
```
TypeError: 'tuple' object does not support item assignment
```
「tuple」は要素の変更が出来ないと怒られる。

### taple同士の比較

比較演算子ですべての要素を比較できる。

```
tuple_sample1 = (1, 2, 3, 4, 5)
tuple_sample2 = (1, 2, 3, 4, 5)

print(tuple_sample1 == tuple_sample2)
```
実行結果
```
True
```

「==」の他にも「!=」や「<」や「>」ですべての要素の大小関係を比較することも出来る。

比較演算子を使うと「True」や「False」のbool値が返ってくる。

### tapleの検索

「in」演算子で要素の検索も可能。

```
tuple_sample = (1, 2, 3, 4, 5)

print(1 in tuple_sample)
```
実行結果
```
True
```

タプルに「1」が含まれているので「True」が返ってくる。

## Python標準のリストとNumPyの配列（NumPy.ndarray）の使い分け

同じ型ばかり扱うときは、基本的に「NumPy.ndarray」を使うのが良い？

Python標準のリストよりも「NumPy.ndarray」の方が処理が高速で、標準のリストで出来ることは大体できるから。

「Numpy.ndarray」は「Numpy」をインポートしないと使えないので注意！

```
import numpy as np
import matplotlib.pyplot as plt
date = np.array(range(1,31))
temp = np.array([
22,25,23,26,21,22,22,
17,20,19,22,26,21,19,
22,20,15,16,22,26,26,
28,19,21,23,25,22,26,
26,26])

plt.plot(date, temp)
plt.xlim([1,31])
plt.ylim([0,40])
plt.show()
```

date（日付）とtemp（気温）をNumPyのリスト（Numpy.ndarray）に格納し、plt.plot(date, temp)でグラフに点と線をまとめて描くコード。


インポート時は基本的に「np」と名付けるのが一般的。
```
import numpy as np
```

## Python標準のリストは異なる型を格納できる？

[Pythonのリストと配列とnumpy\.ndarrayの違いと使い分け \| note\.nkmk\.me](https://note.nkmk.me/python-list-array-numpy-ndarray/)

簡単な処理は「Python標準のリスト」、算術的な計算をしたい場合は「numpy.ndarray」って感じの使い分けでOK。

数字だけの多次元配列とか使うときは「numpy.ndarray」が楽。

## エラーが出たら

ググれば大体出てくるけど、よくあるエラーはこのページとかが参考になる。

「プログラミングをやる上で勉強すべき言語は英語」っていうのは割とマジ。

[Pythonエラー一覧（日本語） \- Qiita](https://qiita.com/soutarrr7/items/84e529d87aa3b3a9adcb)
