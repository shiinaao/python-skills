# 列表去重

## 用集合

```
In [1]: li = ['b','c','d','b','c','a','a']

In [2]: list(set(li))
Out[2]: ['b', 'd', 'c', 'a']
```

## 利用 dict key 唯一

```
In [3]: dict.fromkeys(li).keys()
Out[3]: dict_keys(['b', 'c', 'a', 'd'])
```

## set 推导式

这种方法可以一并对元素进行处理

```
In [4]: list({i+'+' for i in li})
Out[4]: ['a+', 'd+', 'c+', 'b+']
```

然后我现在需要保持原顺序的去重, 上面的任一方法去重之后在排序就好, 比如

```
In [6]: li = ['b','c','d','b','c','a','a']

In [7]: l2 = list(set(li))
   ...: l2.sort(key=li.index)
   ...: 

In [8]: print(l2)
['b', 'c', 'd', 'a']
```

## 万能解法\(列表推导式\)

```
In [9]: li = ['b','c','d','b','c','a','a']

In [10]: l2 =[]
    ...: [l2.append(i+'+') for i in li if i+'+' not in l2]
    ...: 
Out[10]: [None, None, None, None]

In [11]: print(l2)
['b+', 'c+', 'd+', 'a+']
```

一行完成了 去重, 保持顺序 和 处理, 有点太极端了, 分开写又不是不能用

# 列表排序

## 两种规则同时排序\(@laike9m\)

```
In [12]: lst = [1, -2, 10, -12, -4, -5, 9, 2]

In [13]: lst.sort(key=lambda x: (x < 0, abs(x)))

In [14]: print(lst)
[1, 2, 9, 10, -2, -4, -5, -12]
```



