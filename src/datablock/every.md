# データの段落分け, every

段落に分けることで異なるデータを一つのファイルに含めることができる.
段落は **1** つの空行で区切る.
段落は block と呼ばれる.
空行を除いた行を point (または column) と呼ぶ.

[index](index.html) もこれとよく似たが異なるデータフォーマットに対した操作を提供している.

## Data Format

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

## `every` keyword

```bash
plot ... every {<point_incr>}
    {:{<block_inr>}
    {:{<start_point>}
    {:{<start_block>}
    {:{<end_point>}
    {:{<end_block>}}}}}}
```

| params        | default | value       | explanation                   |
|---------------|---------|-------------|-------------------------------|
| `point_incr`  | 1       | (int) index | 読む point (行) のステップ    |
| `block_inr`   | 1       | (int) index | 読む block のステップ         |
| `start_point` | 0       | (int) index | 読む point の最初 (0-indexed) |
| `start_block` | 0       | (int) index | 読む block の最初 (0-indexed) |
| `end_point`   | last    | (string)    | 読む point の最後             |
| `end_block`   | last    | (string)    | 読む block の最後             |

例えば、 1 番目のブロック (0-start) のみ指定するには
`every :::1::1`
とする
(何度も言うがこれなら `index` の方が分かりやすいし良い).

## Example

### Source Code

```bash
plot 'blocks.dat' every :::0::0 lc rgb "#0000ff" w lp title 'data1' ,\
     'blocks.dat' every :::1::1 lc rgb "#00ff00" smooth bezier title 'data2'
```

### Data (blocks.dat)

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

![](https://i.imgur.com/FMLpzjT.png)
