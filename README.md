# グラフ理論

## 参照

 - [例題で学ぶグラフ理論(Amazon Link)](https://www.amazon.co.jp/dp/4627052812)
 - [Matching Documentation(Library)](https://matching.readthedocs.io/en/latest/index.html)

***

## 定義

1. 集合
2. グラフ
3. 多重グラフ
4. 順序対
5. 有効グラフ
6. 部分集合
7. 部分グラフ
8. 写像
9. グラフの同型
10. 集合の和, 積
11. 次数
12. 有効グラフの次数
13. 正則グラフ
14. 歩道, 道, 閉路
15. 有向道, 有向閉路
16. 切断点, 橋
17. 内素な道
18. 距離, 直径

***

# 定義1 : 集合とは

集合：異なるものの集まり  

Pythonには組み込み関数として`set()`が用意されている。これは集合という意味であり、データは`{}（波括弧）`に囲われて表現される。また集合ではデータが一意に扱われる。

```python
X = {"a", "b", "c"}
print(type(X))
# <class 'set'>

Y = ["a", "a", "b", "c"]
print(set(Y))
# {"a", "b", "c"}
```

上記のように配列`Y`に`a`が2つ含まれている、つまり重複している場合は`set()`により一意なデータとして変換される。ここで集合に格納された値のことを**要素**、あるいは**元**という。ここでは「`a`, `b`, `c`」が要素である。また、要素が一つもないことを**空集合**といい、要素数が有限の場合は**有限集合**、無限の場合は**無限集合**と呼ぶ。

集合は`X = {1, 2, 3, 4}`のように要素を表現することもあるが、要素の性質を用いて`X = {x|xは4以下の自然数}`と表すこともできる。Pythonで表すとおおよそ以下で正しいだろう。また**n元集合**とは要素数をnとした時の有限集合のことである。
```python
X = {1, 2, 3, 4}
X = lambda x: True if x <= 4 else False
```

### 用語
 - 集合
 - 要素, 元
 - 空集合
 - 有限集合
 - 無限集合
 - n元集合 

*** 

# 定義2 : グラフ

グラフ : 頂点と辺からなるもの

グラフとは頂点（点）の集合（**頂点集合**）と辺の集合（**辺集合**）によって構成される。頂点集合、辺集合がともに有限であるものを**有限グラフ**という。グラフの頂点の数は**位数**と呼ばれ、グラフの辺の数は**サイズ**と呼ばれる。

<img src="./img/graph_2.png">

以下はグラフを通しての理解が効率的だと判断したため箇条書きで記している（太字部分が新しい用語）。カッコの中は各用語の説明である。

 - aとbは**隣接**（辺を成している）
 - cとdは**非隣接**（辺を成していない）
 - 辺adの**端点**は頂点a, d（辺を構成している頂点）
 - 頂点dの**近傍**は頂点a, b（自身の頂点と辺を成している頂点）
 - 頂点aに**接続している**辺は、ab, ac, ad（自身が辺を構成する一部である）

### 用語
 - グラフ
 - 頂点, 点, 端点
 - 頂点集合
 - 辺集合
 - 有限グラフ
 - 位数
 - サイズ
 - 隣接する
 - 接続する
 - 近傍

***

# 定義3 : 多重グラフ

多重グラフ : 多重辺やループを許したグラフ

**多重辺**とは2頂点を結ぶ辺が2本以上ある辺のこと。例えば頂点a, bで辺を成すものが2本あり、それぞれの辺の名前を「A, B」としたとき「A, B」はともに多重辺である。つまり、辺を構成する端点が同一のものが2本以上ある場合のこと。次に**ループ**だが、これは端点が同じ辺のこと。また、多重辺やループを持たないグラフを**単純グラフ**、あるいは単にグラフと呼ぶ。定義2のグラフは単純グラフである。

<img src="./img/graph_3.png">

### 用語
 - 多重辺
 - ループ
 - 多重グラフ
 - 単純グラフ

***

# 定義4 : 順序対

順序対 : 決められた順序に並べられた対象の対

**順序対**は`(a, b)`で表され、a, bそれぞれを第一成分、第二成分と呼ぶ。aとbの値が異なる場合`(a, b)`と`(b, a)`は異なる順序対である。順序対とは要するに、多重グラフにおける多重辺に順序が加えられたものだと考えればよい。また、`(a, a)`となる順序対も存在する。  
順序対は次の定義5で扱われる。

```python
a = 10
b = 20

X = (a, b)
Y = (b, a)

print(X == Y)
# False
```

### 用語
 - 順序対

***

# 定義5 : 有向グラフ

有向グラフ : 辺に向きのあるグラフ

辺に向きのあるグラフのことを**有向グラフ**（ダイグラフ）と呼び、頂点集合と**弧**（有向辺）と呼ばれる頂点の順序対の集合（弧集合）によって構成される。

<img src="./img/graph_5.png">

有向グラフに対して、向きのないグラフを**無向グラフ**、あるいは単にグラフと呼ぶ。これまで扱っていたのは無効グラフである。上の図で`(a, b)`と`(b, a)`は順序対であり、第一成分は**始点**、第二成分は**終点**とよばれる。また、`(a, b)`と`(b, a)`は**対象弧**でもある。さらに、同一の`(始点、終点)`を持つ2本以上の弧を**多重弧**と呼ぶ。ここでは`(d, a)`の弧が2本以上あるため、これは多重弧である。  
多重弧やループを許した有向グラフを**多重有向グラフ**、あるいは**多重ダイグラフ**と呼び、多重辺やループを持たないグラフを**単純有向グラフ**、あるいは単に有向グラフ（ダイグラフ）と呼ぶ。上の図は多重有向グラフである。また。定義2のグラフに順序がついたものが単純有向グラフである。

### 用語
 - 有向グラフ, ダイグラフ
 - 弧, 有向辺
 - 弧集合
 - 無向グラフ
 - 始点
 - 終点
 - 対象弧
 - 多重弧
 - 多重有向グラフ, 多重ダイグラフ
 - 単純有向グラフ

***

# 定義6 : 部分集合

以下の`A`は要素として`1, 3, 5`を有しており、`B`は`A`の要素に加え、`2, 4`の要素を有している。この時`B`は`A`の要素を含んでおり、これを`A`は`B`の**部分集合**であると表現する。また、空集合は任意の集合の部分集合である。

```python
A = {1, 3, 5}
B = {1, 2, 3, 4, 5}

C = A & B

print(A == C)
# True
```

### 用語
 - 部分集合

***

# 定義7 : 部分グラフ

部分グラフ : 元となるグラフの一部となるグラフ

**部分グラフ**とは、元となるグラフがあり、その一部であるグラフのこと。とくに、頂点が完全に一致しているものを**全域部分グラフ**と呼ぶ。さらに**誘導部分グラフ**とは、ある頂点を基準にしたときに、その頂点が構成する辺が、すべて元のグラフに含まれている時を指す。

<img src="./img/graph_7.png">

### 用語
 - 部分グラフ
 - 全域部分グラフ
 - 誘導部分グラフ

***

# 定義8 : 写像

写像 : 集合から集合へ要素を対応させること

<img src="./img/graph_8.png">

上の図をもとに写像について説明する。集合Xは要素`{A, B, C, D}`を有している。集合Yは要素`{1, 2, 3}`を有している。ここでは分かりやすくするために、結婚相手を考えるものとする。集合Xは女性の集団であり、呼称を各要素に「さん」をつけて呼ぶこととする（例：Aさん）。集合Yも同様の呼称とする。この時、例えばAさんは1さんと結婚したいと考えており、これは以下のプログラムでのAさんの値1と対応する。この値を使い`(A, 1)`とすることをAから1への**写像**という。ここでは左から右への向きを持つ。  

次に、2さんは自分と結婚したい人がいるかどうか確認したいとする。その場合は、自分の「2」という名前を使い、女性の集団から自分と結婚したい人を探すことになる。そうするとBさんとDさんがいることになる。矢印とは逆方向（右から左）から「対応する要素が存在すること」を**上への写像**という。

次に、集合Xのどの2個の要素も集合Yの異なる要素に対応するとき、つまり結婚相手がかぶらないとき、XからYへの**1対1の写像**という。ここでは集合XからAさんとBさんで1対1の写像となっている。

```python
X = {
    "A": 1,
    "B": 2,
    "C": 3,
    "D": 2,
}

Y = {1, 2, 3}


def func(z):
    for i in z:
        for k, v in X.items():
            if v == i:
                print(f"{i}さんと結婚したい人には{k}さんがいる")

func(Y)
# - Result - 
# 1さんと結婚したい人にはAさんがいる
# 2さんと結婚したい人にはBさんがいる
# 2さんと結婚したい人にはDさんがいる
# 3さんと結婚したい人にはCさんがいる
```

### 用語
 - 写像
 - 上への写像
 - 1対1の写像

***

# 定義9 : グラフの同型

グラフの同型 : 「同一」の頂点を持ち、同一の辺の繋がり方をしているグラフ

グラフを並び変えたり、回転させたりすることで、同じグラフが存在する場合のこと。以下のグラフで左のグラフと真ん中のグラフは同型ではなく、同型なのは左と右のグラフである。

<img src="./img/graph_9_1.png">

また、以下のグラフは片方を並び変えることで、もう片方のグラフと同じ形を作ることができるため同型である。

<img src="./img/graph_9_2.png">

### 用語
 - 同型
