# 二维数组\(矩阵\)

```
In [1]: a = [[1,2,3], [4,5,6],[7,8,9]]

# 1 2 3 
# 4 5 6
# 7 8 9
```

组合 zip 和 reversed, 想怎么转就怎么转, 只展示3个例子

## 顺指针旋转90度

```
In [2]: list(zip(*reversed(a)))
Out[2]: [(7, 4, 1), (8, 5, 2), (9, 6, 3)]

# 7 4 1
# 8 5 2
# 9 6 3
```

## 逆时针旋转90度

```
In [3]: list(reversed(list(zip(*a))))
Out[3]: [(3, 6, 9), (2, 5, 8), (1, 4, 7)]

# 3 6 9
# 2 5 8
# 1 4 7
```

## 顺时针180度

```
In [4]: map(reversed, reversed(a))
Out[4]: <map at 0x4f669e8>

# 生成器也是醉了
In [5]: list(map(lambda x:list(reversed(x)), list(reversed(a))))
Out[5]: [[9, 8, 7], [6, 5, 4], [3, 2, 1]]

# 9 8 7
# 6 5 4
# 3 2 1
```



