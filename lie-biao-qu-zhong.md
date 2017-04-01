## 用集合

```
li = ['b','c','d','b','c','a','a']

list(set(li))
Out[3]: ['b', 'a', 'd', 'c']
```

## 利用 dict key 唯一

```
dict.fromkeys(li).keys()
Out[6]: dict_keys(['b', 'd', 'c', 'a'])
```

## set 推导式

这种方法可以一并对元素进行处理

```
list({i+'+' for i in li})
Out[8]: ['a+', 'b+', 'd+', 'c+']
```

然后我现在需要保持原顺序的去重, 上面的任一方法去重之后在排序就好, 比如

```
li = ['b','c','d','b','c','a','a']

l2 = list(set(li))
l2.sort(key=li.index)
print(l2)
# ['b', 'c', 'd', 'a']
```

## 万能解法\(列表推导式\)

```
li = ['b','c','d','b','c','a','a']
l2 =[]
[l2.append(i+'+') for i in li if i+'+' not in l2]
# Out[36]: [None, None, None, None]
print(l2)
# ['b+', 'c+', 'd+', 'a+']
```

一行完成了 去重, 保持顺序 和 处理, 有点太极端了, 分开写又不是不能用

