# 字典合并

## 常见写法

```
z = dict(x.items() + y.items())  # py2

# 类似的写法py3 稍微有点不同
z = dict(list(x.items()) + list(y.items()))  # py3
```

## deep copy

```
z = x.copy()
z.update(y)
```

## 魔幻的一行式

```
# 注意除了第一个dict以外, 其他的都要加 **, 进行kw解析
dictMerged2=dict(dict1, **dict2)
```

# 字典排序

py3.6 版本之后的 dict 实现是有序的, 在这之前的版本需要有序字典, 可以使用`collections.OrderedDict` 类

## 使用 lambda

```
da = {1: 2, 3: 4, 4:3, 2:1, 0:0}
sorted(da.items(), key=lambda x: x[1])
# Out[10]: [(0, 0), (2, 1), (1, 2), (4, 3), (3, 4)]

from collections import OrderedDict
OrderedDict((sorted(da.items(), key=lambda x: x[1])))
# Out[16]: OrderedDict([(0, 0), (2, 1), (1, 2), (4, 3), (3, 4)])
```

## 毫无存在感的方法二

```
import operator
sorted(x.items(), key=operator.itemgetter(1))
# Out[17]: [(0, 0), (2, 1), (1, 2), (4, 3), (3, 4)]
```



