# 横向き棒グラフ

## 概要

横向きの棒グラフを描画したい.
通常の `with boxes` による棒グラフの描画は必ず縦向きであるが
カテゴリカルデータであって x 軸にラベルを表示する場合,
そのラベルが長いとラベル同士が重なったり見切れてしまい見づらい.
y 軸にラベルを表示して棒グラフを横向き（水平方向）にすることでこれを解決する.

![](https://i.imgur.com/AtUimHD.png)

これを

![](https://i.imgur.com/CSRcoGq.png)

こうしたい.

## 参考

- [Horizontal bar chart in gnuplot - Stack Overflow](https://stackoverflow.com/questions/62848395/horizontal-bar-chart-in-gnuplot)
- [boxxyerror - gnuplot](http://www.gnuplot.info/docs_6.0/loc4843.html)

## 手法

直接に横向きの棒グラフを描画する機能は gnuplot にはない.
ただし比較的自由に矩形を描画することは `with boxxyerror` を使うことで可能.
これを利用（悪用）して横向きの棒グラフを描画する.

## Example

### データ (data.txt)

```
apple 100
banana 200
candy 250
```

### Source Code

```bash
set terminal pngcairo size 800,600 enhanced font "Arial,12"
set output 'test.png'

# tics style
set style line 11 lc rgb '#808080' lt 1 lw 3
set border 0 back ls 11
set tics out nomirror
set style line 12 lc rgb '#808080' lt 0 lw 1

# grid style
set grid back ls 12

# box style
set style fill solid 0.5 border lc rgb '#55aaff'
set style line 1 lc rgb '#77ccff'

set yrange [0:*]
set xrange [0:*]
set style fill solid
unset key

myBoxWidth = 0.9
set offsets 0,0,0.5-myBoxWidth/2.,0.5

plot 'data.txt' using (0.5*$2):0:(0.5*$2):(myBoxWidth/2.):ytic(1) with boxxyerror fillcolor ls 1
```
