## 可变默认参数 - [原文地址](http://pythonguidecn.readthedocs.io/zh/latest/writing/gotchas.html#default-args)

看起来，最 让Python程序员感到惊奇的是Python对函数定义中可变默认参数的处理。

你所写的

```
def append_to(element, to=[]):
  to.append(element)
  return to
```

你所期望的

```
my_list = append_to(12)
print my_list
​
my_other_list = append_to(42)
print my_other_list
```

每次调用函数时，如果不提供第二个参数，就会创建一个新的列表，所以结果应是这样的：

```
[12] [42]
```

而事实是

```
[12]
[12, 42]
```

当函数被定义时，一个新的列表就被创建 一次 ，而且同一个列表在每次成功的调用中都被使用。

当函数被定义时，Python的默认参数就被创建 一次，而不是每次调用函数的时候创建。 这意味着，如果你使用一个可变默认参数并改变了它，你 将会 在未来所有对此函数的 调用中改变这个对象。

你应该做的在每次函数调用中，通过使用指示没有提供参数的默认参数（None 通常是 个好选择），来创建一个新的对象。

```
def append_to(element, to=None):
  if to is None:
  to = []
  to.append(element)
  return to
```

什么情况下陷阱不是陷阱有时你可以专门“利用”（或者说特地使用）这种行为来维护函数调用间的状态。这通常用于 编写缓存函数。

