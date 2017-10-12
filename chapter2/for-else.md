万万没想到, 在 Python 这门缩进严格的语言中, if else 这一对儿竟然有缩进不统一的写法
> **ps**: Effective Python 中第12条解释, `else`可以写在`for`和`while`语句后面, 但是不推荐这样做

这段代码是在 V2EX 上看到的

```
for i in range(88):
    if i > 80:
        print(i)
        break
#这里遍历一个列表元素是否满足条件
else:
    print('go')
# 如果全部都不满足条件会跳转执行这一步

# Out: 81
```

然后把 88 改成 小于 80 的数试试

```
for i in range(8):
    if i > 80:
        print(i)
        break
else:
    print('go')

# Out: go
```

但是这种写法太魔幻了, 不易理解, 所以推荐使用下面的写法

```
li = range(88)
res = filter(lambda x: x > 80, li)
if res:
    print(list(res))
else:
    print(go)

# Out: [81, 82, 83, 84, 85, 86, 87]
```



