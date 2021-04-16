# エラーバー, 誤差付きプロット, yerrorbars

## 参考

- [http://dsl4.eee.u-ryukyu.ac.jp/DOCS/gnuplot/node158.html](http://dsl4.eee.u-ryukyu.ac.jp/DOCS/gnuplot/node158.html)

## 概要

y軸方向にエラーバーについたプロットを行う.
エラーの大きさ（半径）を指定する方法と, 上限と下限のそれぞれを指定する方法の二つがある.

## `with yerrorbars`

次のいずれか.

```bash
plot ... using {<x>:}<y>:<ydelta> with yerrorbars
plot ... using <x>:<y>:<ylow>:<yhigh> with yerrorbars
```

| params   | default | value      | explanation                                  |
|----------|---------|------------|----------------------------------------------|
| `x`      | --      | (double) x | x 座標                                       |
| `y`      | --      | (double) y | エラーバーの中点 y 座標                      |
| `ydelta` | --      | (double)   | これのプラスマイナスを `ylow` `yhigh` とする |
| `ylow`   | --      | (double)   | エラーバーの下点 y 座標                      |
| `yhigh`  | --      | (double)   | エラーバーの上点 y 座標                      |

## Examples

### ydelta

ydelta \\( \Delta \\) を指定する場合は \\( y \pm \Delta \\) をエラー範囲とする.

```bash
$data << EOM
-5 -10 2.5
-4 -8 1.6
-3 -6 0.9
-2 -4 0.4
-1 -2 0.1
0 0 0.0
1 2 0.1
2 4 0.4
3 6 0.9
4 8 1.6
EOM

set grid
plot $data u 1:2:3 with yerrorbars
```

![](https://i.imgur.com/3S0qvEb.png)
