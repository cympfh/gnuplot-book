# 等高線

## 方法

```bash
set contour
unset surface
set view 0, 0

set isosamples 100
set cntrparam levels 9

set key out

splot x**2 - y**2
```

![](https://i.imgur.com/Quhsylf.png)
