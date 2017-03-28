python 中 dict 的 setdefault\(\) 方法, 可以给字典添加一条内容

```
def setdefault(self, k, d=None): # real signature unknown; restored from __doc__
        """ od.setdefault(k[,d]) -> od.get(k,d), also set od[k]=d if k not in od """
        pass
```

若k 在字典中不存在, 则添加内容, 不指定d 的情况下, value 默认为 None 

若k 在字典中存在, 不论其value 的值是不是None 都不进行操作**setdefault\(\)方法可以用于保护字典中的数据**

```
da = {'name':'homer', 'age':20}

da.setdefault('age', -1)
Out[5]: 20

print(da)
{'name': 'homer', 'age': 20}

da.setdefault('status', 'run')
Out[8]: 'run'

print(da)
{'name': 'homer', 'status': 'run', 'age': 20}
```



