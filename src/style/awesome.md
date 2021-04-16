# awesome style

```bash
set terminal pngcairo

set style line 1 lw 2 pt 6 lc rgb "#00aaaa"

set style line 11 lc rgb '#808080' lt 1 lw 3
set border 0 back ls 11
set tics out nomirror

set style line 12 lc rgb '#808080' lt 0 lw 1
set grid back ls 12

set xrange [-4:4]
plot x**3 linestyle 1
```

![result](https://i.imgur.com/q5HVo7E.png)

gnuplot はそのまま使うと一見して gnuplot で作ったダサい見た目になりがち.
小洒落たスタイルでライバルに差をつけろ.
