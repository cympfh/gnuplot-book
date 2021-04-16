# ヒートマップ, 混合行列

## 参考

- [gnuplot demo script: heatmaps.dem](http://gnuplot.sourceforge.net/demo_svg/heatmaps.html)

## 概要

混合行列 (Confusion Matrix) などと呼ばれるあの表を色付きで図示する.
色の濃さで数の大きさを表現する.

上の参考リンクでは色が連続して変化するように中間値補完が為されてるが,
私の知ってるgnuplotのバージョンではこれは再現できない.
これをするには `pm3d` を使ったほうがいいと思う.

![](https://i.imgur.com/8FJ6kh9.png)

## 方法

### Data Format

行列 (`matrix`) 形式でデータを与えることにする.
すなわち, データ $z$ を $n$ 行 $m$ 列に並べたものをデータとする.

```dat
z11 z12 z13
z21 z22 z23
z31 z32 z33
z41 z42 z43
```

混合行列を図示する目的のためには行と列とに見出し (座標ではなくラベル) があるべきで,
どうせならデータに含めたい.
gnuplot の matrix data は行ごとのアイテム数は揃ってる必要があるので,
0行目0列目にはダミーデータを入れた上で,
1行目または1列目に見出しを入れられる.

```dat
xxxx Col1 Col2 Col3
Row1  z11  z12  z13
Row2  z21  z22  z23
Row3  z31  z32  z33
Row4  z41  z42  z43
```

### `with image`

```bash
plot ... using <x>:<y>:<z> with image
```

| params           | default       | value          | explanation |
| :--------------- | :-----------: | :------------- | :---------- |
| `x` | -- | (int)     | データの $x$ 座標 |
| `y` | -- | (int)     | データの $y$ 座標 |
| `z` | -- | (double)  | データ. 対応する色が塗られる |

ただし, matrix で読む場合は `x`, `y` は自動的に column 1, 2 として適切な値が入ってると見なしてよい.

### `columnheaders`, `rowheaders`

```bash
plot ... matrix column rowheaders
```

データの一行目, 一列目の文字列を見出しだと思って,
二行目, 二列目以降のデータだけを使う.

### Example

```bash
$data << EOM
xxxx Col1 Col2 Col3
Row1    1    2    3
Row2    2    4    6
Row3    4    8   12
Row4    8   16   24
EOM

unset key
set title 'Heatmap with image'

set cbrange [0:30]  # the range of colorbox
set palette cubehelix start -2 cycles 0 saturation 3 gamma 3 negative  # color scheme

plot $data matrix rowheaders columnheaders u 1:2:3 with image ,\
        '' matrix rowheaders columnheaders u 1:2:(sprintf("%g", $3)) with labels
```

![](https://i.imgur.com/L1QEXwC.png)

## 格子線 (gridline)

`set grid` によってセル同士の境界に線を引きたい.
デフォルトだとセルの色塗りは gridline の後に行われて上書きされるので `set grid front` とする.
`lt` や `lc`, `lw` で線のスタイルは調整する.

```bash
$data << EOD
X a b c d e
A 0.0 -0.06 -0.25 -0.56 -1.0
B 0.11 0.04 -0.13 -0.45 -0.88
C 0.44 0.38 0.19 -0.11 -0.55
D 1.0 0.93 0.75 0.43 0.0
E 1.77 1.71 1.52 1.21 0.77
EOD

set grid front lw 1.5 lt -1 lc rgb 'white'
plot $data matrix rowheaders columnheaders w image not
```

![](https://i.imgur.com/08eJtZ7.png)

`xy` に gridline を引いてもちょうど 0.5 ずれた, セルの真ん中に引くようになってしまう.
なぜならセルはちょうど格子点 \\( (x, y) \\) に対して, \\( (x-0.5, y-0.5) \ldots (x+0.5, y+0.5) \\)
という矩形領域を占めているためである.

ちょうど 0.5 ずらした格子線を手に入れるために小目盛り (minor tics) を利用する.
ただし `xy` の大目盛りがラベルのために使われている (数値で指定されていない) ときは小目盛りは使えないことになっているので,
`x2y2` を使う.

まず `x2, y2` を宣言し `set link` で `xy` と同期させる.
これに小目盛り `mx2, my2` を `interval=2` で宣言することで, ちょうど半分に分割する目盛りを作れる.
`grid` の引数に `mx2tics, my2tics` を追加すればよい.

変更点だけ書き出すと次の通り.

```diff
+set x2tics
+set y2tics
+set link x2
+set link y2
+set mx2tics 2
+set my2tics 2
-set grid front lw 1.5 lt -1 lc rgb 'white'
+set grid front mx2tics my2tics lw 1.5 lt -1 lc rgb 'white'
```

最後に余計なラベルや刻み線を消す処理を追加して結局

```bash
$data << EOD
X a b c d e
A 0.0 -0.06 -0.25 -0.56 -1.0
B 0.11 0.04 -0.13 -0.45 -0.88
C 0.44 0.38 0.19 -0.11 -0.55
D 1.0 0.93 0.75 0.43 0.0
E 1.77 1.71 1.52 1.21 0.77
EOD

set xtics scale 0  # 刻み線の長さ
set ytics scale 0
set x2tics format '' scale 0.01  # こちらもゼロにしたいがすると格子線まで消えてしまうので
set y2tics format '' scale 0.01
set link x2
set link y2
set mx2tics 2
set my2tics 2
set grid front mx2tics my2tics lw 1.5 lt -1 lc rgb 'white'
plot $data matrix rowheaders columnheaders w image not
```

![](https://i.imgur.com/LFQu9gC.png)

となった.
