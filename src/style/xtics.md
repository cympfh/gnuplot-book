# xtics

ytics も全く同様

## Reference

- [Xtics - docs_4.2](http://gnuplot.sourceforge.net/docs_4.2/node295.html)

## 刻み幅の指定

目盛りの刻み幅を指定する.

```bash
set xtics 5
```

![](https://i.imgur.com/wR7BauF.png)

## 目盛りラベルの回転

```bash
set xtics rotate by 30 right
```

角度 (deg) とどこを中心に回転するかの指定.
角度は反時計回りで, 負数で時計回りに回せる.
`right` キーワードでラベルの右端を中心に回転することを指定する.
省略すると左端を中心に回転する.

### Example

```bash
set xtics rotate by 30 right
set xrange [-100:100]
plot x title "rotate by 30 right"
```

![](https://i.imgur.com/GPLvsY5.png)

## ラベル文字列の指定

ラベル文字列と座標の組のリストを与えることで, 数字付きの tics じゃなくてラベル文字列を指定した座標に置く事ができる.

```bash
set xtics ("label1" x1, "label2" x2, "label3" x3)
```

### Example

```gnuplot
set xrange [0:6]
set xtics ("zero" 0, "two" 2, "last" 6)
set grid
plot x
```

![](https://i.imgur.com/5oatvRz.png)
