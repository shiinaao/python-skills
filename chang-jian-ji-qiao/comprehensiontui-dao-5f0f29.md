# 推导式\(快\)

总有人和我说可以一个`for` 或者一个`if` 解决问题, 那为什么要用`推导式` 呢?  

不只是因为写成一行显得比较酷, 更重要的是**快**

```
def ff():
    li = []
    for i in range(10000):
        li.append(i)
        

%timeit ff()
# The slowest run took 5.21 times longer than the fastest. This could mean that an intermediate result is being cached.
# 1000 loops, best of 3: 817 µs per loop

%timeit [i for i in range(10000)]
# The slowest run took 4.48 times longer than the fastest. This could mean that an intermediate result is being cached.
# 1000 loops, best of 3: 340 µs per loop
```

## list - 列表推导式 =&gt; \[\]

```
[i**2 for i in range(5)]
# Out[3]: [0, 1, 4, 9, 16]
```

## dict - 字典推导式 =&gt; {}

```
{i: i**2 for i in range(5)}
# Out[11]: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## set - 集合推导式\(这个真的不是括号\) =&gt; {}

```
{i**2 for i in [1,2,3,1,2,3]}
# Out[9]: {1, 4, 9}
```

## generator - 生成器推导式 =&gt; \(\)

```
(i**2 for i in [1,2,3,1,2,3])
# Out[12]: <generator object <genexpr> at 0x0000000004F54830>

list((i**2 for i in [1,2,3,1,2,3]))
# Out[13]: [1, 4, 9, 1, 4, 9]
```



