## 强制转换到指定变量的类型

在 Fluent Python 中 14.8 章中提到了这种写法

```python
In [1]: source = []

In [2]: target = '123'

In [3]: type(source)(target)
Out[3]: ['1', '2', '3']

In [4]: source = ()

In [5]: type(source)(target)
Out[5]: ('1', '2', '3')

In [6]: source = 1

In [7]: type(source)(target)
Out[7]: 123

```

使用 `type(source)(target)` 将`target`转换为`source`的类型(source, target 已声明)

如果无法转换到目标类型, 则会抛出异常