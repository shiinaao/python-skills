## 迟绑定闭包 - [原文地址](http://pythonguidecn.readthedocs.io/zh/latest/writing/gotchas.html#id8)

另一个常见的困惑是Python在闭包\(或在周围全局作用域（surrounding global scope）\)中 绑定变量的方式。

你所写的

```
def create_multipliers():
  return [lambda x : i * x for i in range(5)]
```

你所期望的

```
for multiplier in create_multipliers():
  print multiplier(2)
```

一个包含五个函数的列表，每个函数有它们自己的封闭变量 i 乘以它们的参数，得到:

```
0
2
4
6
8
```

而事实是

```
8
8
8
8
8
```

五个函数被创建了，它们全都用4乘以 x 。

Python的闭包是 迟绑定 。 这意味着闭包中用到的变量的值，是在内部函数被调用时查询得到的。

这里，不论 任何 返回的函数是如何被调用的， i 的值是调用时在周围作用域中查询到的。 接着，循环完成， i 的值最终变成了4。

关于这个陷阱有一个普遍严重的误解，它被认为是和Python的 lambdas 有关。 由 lambda 表达式创建的函数并没什么特别， 而且事实上，同样的问题也出现在使用普通的 定义 上：

```
def create_multipliers():
  multipliers = []
​
  for i in range(5):
  def multiplier(x):
  return i * x
  multipliers.append(multiplier)
  return multipliers
```

你应该做的最一般的解决方案可以说是有点取巧（hack）。由于Python拥有在前文提到的为函数默认参数 赋值的行为（参见 可变默认参数 ）,你可以创建一个立即绑定参数的闭包,像下面这样：

```
def create_multipliers():
  return [lambda x, i=i : i * x for i in range(5)]
```

或者，你可以使用 functools.partial 函数：

