# 推导式\(快\)

总有人和我说可以一个`for` 或者一个`if` 解决问题, 那为什么要用`推导式` 呢?

不只是因为写成一行显得比较酷, 还有一个原因是**快**, 下面的例子展示的是**碾平列表的正确方式**

```
In [11]: li = [[1,2,3], [4,5], [6,7,8]]

In [12]: def ff():
    ...:     res = []
    ...:     for i in li:
    ...:         for j in i:
    ...:             res.append(j)
    ...:     return res
    ...: 

In [13]: %timeit ff()
1.38 µs ± 1.61 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)

In [14]: %timeit [j for i in li for j in i]
833 ns ± 1.36 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)
```

原因应该是推导式没有`.append()` 省去了`getattr` 的时间

## list - 列表推导式 =&gt; \[\]

```
In [15]: [i**2 for i in range(5)]
Out[15]: [0, 1, 4, 9, 16]
```

举个高级点的例子, 查找某目录及其子目录下所有`.md`后缀的文件

```
import os

li = [os.path.join(root, file)
        for root, dirs, files in os.walk('D:\\Users\\Administrator\\Desktop\\test')
        for file in files if file.endswith('.md')]

print(li)
# ['D:\\Users\\Administrator\\Desktop\\test\\1.md', 'D:\\Users\\Administrator\\Desktop\\test\\e\\a\\2.md']
```

## dict - 字典推导式 =&gt; {}

```
In [6]: {i: i**2 for i in range(5)}
Out[6]: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## set - 集合推导式\(这个真的不是括号\) =&gt; {}

```
In [7]: {i**2 for i in [1,2,3,1,2,3]}
Out[7]: {1, 4, 9}
```

## generator - 生成器推导式 =&gt; \(\)

```
In [9]: (i**2 for i in [1,2,3,1,2,3])
Out[9]: <generator object <genexpr> at 0x00000000050EA468>

In [10]: list((i**2 for i in [1,2,3,1,2,3]))
Out[10]: [1, 4, 9, 1, 4, 9]
```



