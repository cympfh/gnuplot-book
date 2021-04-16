# シェルの実行

`<` から始まる文字列を plot の対象にすると, gnuplot はこれをシェルコマンドとして実行して, その標準出力を用いる.

## Example

### seq

`seq 100` は 1 から 100 までの整数を 100 行で出力する.
これをデータと思えば次のような事ができる.

```bash
plot '<seq 100' ,\
     '<seq 100' u 1:($1*sin($1/pi)) smooth bezier
```

### データのフィルタ

次のようなテキストファイル (`data.txt`) があるとする.

```
A 3
B 10
A 4
B 11
A 5
B 12
```

このときに `A` のある行だけのプロット, `B` の行のプロットを行うには, `grep` によるフィルタを利用すればよい.

```bash
plot '< grep A data.txt' title 'A' ,\
     '< grep B data.txt' title 'B'
```

