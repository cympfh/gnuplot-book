# 点の周りにスペースを空ける, pointinterval

## 概要

`with linespoints` のときに点を線でつないで描画されるがそのとき点の周りに少しスペースを空ける事ができる.
これを実現するには,
`pointinterval (pi)` で `-1` を指定して, `set pointintervalbox` でスペースの大きさを指定すると実現できる.

## Example
```bash
set style line 1 pi -1
set style line 1 pt 6  # 点を丸にする
set pointintervalbox 3  # 点と線をあける距離

$data << EOD
1
3
5
6
7
EOD
plot $data w lp ls 1
```

![](https://i.imgur.com/Pjq3VYe.png)
