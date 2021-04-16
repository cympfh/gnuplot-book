# データの段落分け, index

段落に分けることで異なるデータを一つのファイルに含めることができる.
段落は **2** つの空行で区切る.
段落は block と呼ばれる.
各 block には名前を与えることが出来る.

`index` はこの内, プロットに用いるブロックを選択することが出来る.
ブロックの指定は番号かまたはデータに名前をつけることでその名前でも指定することもできる.

[every](every.html) はコレとよく似ているが異なるデータフォーマットに対してより細かなデータの指定が出来る.

## Data Format

データは **2行** の空行で区切る.
データは先頭から 0-start の index が与えられる.
データの先頭にコメントで名前 (`<data_name>`) を与えられる.

```dat
# data1
x1 y1
x2 y2
x3 y3


# data2
x1 y1
x2 y2
x3 y3
```

## `index` keyword

次の2種類の使い方がある.

```bash
plot ... index <start_index>{:<end_index>{:<index_incr>}}
plot ... index <data_name>
```

| params        | default     | value       | explanation                                             |
|---------------|-------------|-------------|---------------------------------------------------------|
| `start_index` |             | (int) index | 読む block の最初 (0-indexed)                           |
| `end_index`   | start_index | (int) index | 読む block の最後 (0-indexed)                           |
| `index_incr`  | 1           | (int)       | start_index から end_index までの範囲にステップを与える |
| `data_name`   |             | (string)    | この名前のデータをプロットに使う                        |

## Example

### Source Code

段落番号 (`start_index`) で指定する方法

```bash
plot 'index.dat' index 0 lc rgb "#0000ff" w lp title 'linear' ,\
     'index.dat' index 1 lc rgb "#00ff00" smooth bezier title 'exp'
```

`data_name` で指定する方法

```bash
plot 'index.dat' index 'linear' lc rgb "#0000ff" w lp title 'linear' ,\
     'index.dat' index 'exp' lc rgb "#00ff00" smooth bezier 'exp'
```

### Data

```
# linear
0 0
1 2
2 4
3 6
4 8
5 10


# exp
0 1
1 2
2 4
3 8
4 16
5 32
```

### Result

![](https://i.imgur.com/8G9GXVI.png)
