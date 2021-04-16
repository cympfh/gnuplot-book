# 散布図

## Data

一点を一行に x, y 座標を並べて記述する.

```
x1 y1
x2 y2
x3 y3
```

## Source Code

オプションなしに `plot` コマンドを使うと散布図がプロットされる.

```bash
$data << EOD
0 0
0 1
1 1
1 2
2 2
EOD

set xrange [-1:3]
set yrange [-1:3]
plot $data pointtype 6
```

## Result
![](https://i.imgur.com/y96sW7e.png)

## テキスト（ラベル）の散布図

ただの点の代わりにテキスト（ラベル）を用いた散布図を作るには
`with labels` を用いる.

```bash
$data << EOD
0 0 A
0 1 B
1 1 C
1 2 D
2 2 E
EOD

set xrange [-1:3]
set yrange [-1:3]
plot $data with labels
```

データの3つ目がデフォルトではラベルとして使われる.

![](https://i.imgur.com/DhM6iXw.png)

```bash
plot $data with labels boxed
```

![](https://i.imgur.com/abJY2Gp.png)
