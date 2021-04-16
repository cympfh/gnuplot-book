# 陰関数

xy 座標上の関数
\\[ f(x,y) = 0 \\]
で表現されるグラフのプロットを考える.

## 手法

三次元グラフとして描画する.
これを \\(z=0\\) 平面で切り取ると目的のグラフが得られる.

## Example

\\(x^2 + xy + y^2 = 1\\) を描画する.
定数を移項することで \\(f(x,y)=0\\) の形にする.

```bash
set view 0,0
unset surface
set isosamples 100,100
set contour
set cntrparam levels discrete 0
set xrange [-2:2]
set yrange [-2:2]

f(x, y) = x * x + x * y + y * y - 1
splot f(x, y)
```

![](https://i.imgur.com/1Wiw7SA.png)
