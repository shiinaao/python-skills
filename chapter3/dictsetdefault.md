# dict.setdefault()

python 中 dict 的 setdefault\(\) 方法, 可以给字典添加一条内容

```
def setdefault(self, k, d=None): # real signature unknown; restored from __doc__
        """ od.setdefault(k[,d]) -> od.get(k,d), also set od[k]=d if k not in od """
        pass
```

若k 在字典中不存在, 则添加内容, 不指定d 的情况下, value 默认为 None 

若k 在字典中存在, 不论其value 的值是不是None 都不进行操作**setdefault\(\)方法可以用于保护字典中的数据**

```
In [1]: da = {'name':'homer', 'age':20}

In [2]: da.setdefault('age', -1)
Out[2]: 20

In [3]: print(da)
{'name': 'homer', 'age': 20}

In [4]: da.setdefault('status', 'run')
Out[4]: 'run'

In [5]: print(da)
{'name': 'homer', 'age': 20, 'status': 'run'}
```

效率上的考虑

```
if key not in my_dict:
	my_dict[key] = []
my_dict[key].append(new_value)

# =================================

my_dict.setdefault(key, []).append(new_value)
```

使用`setdefault()`只需要一次键查询就可以完成操作, 手动判断的话就需要3次键查询

