Python 中创建大量的类实例时, 使用`__slots__`节省内存的使用

Python Cookbook 也稍微提到了一点 [8.4 创建大量对象时节省内存方法](http://python3-cookbook.readthedocs.io/zh_CN/latest/c08/p04_save_memory_when_create_large_number_instances.html)

## 使用时`__slots__`时需要注意的几点：

1. 当一个类的父类没有定义`__slots__`属性，父类中的`__dict__`属性总是可以访问到的，所以只在子类中定义`__slots__`
   属性，而不在父类中定义是没有意义的。
2. 如果定义了`__slots__`属性，还是想在之后添加新的变量，就需要把`__dict__`字符串添加到`__slots__`的元组里。
3. 定义了`__slots__`属性，还会消失的一个属性是`__weakref__`，这样就不支持实例的weak reference，如果还是想用这个功能，同样，可以把`__weakref__`字符串添加到元组里。
4. `__slots__`功能是通过`descriptor`实现的，会为每一个变量创建一个`descriptor`。
5. `__slots__`的功能只影响定义它的类，因此，子类需要重新定义`__slots__`才能有它的功能。

关于`descriptor`详细内容参考: [python中基于descriptor的一些概念（上）](http://www.cnblogs.com/btchenguang/archive/2012/09/17/2689146.html#WizKMOutline_1347874388282794)

## Example

```
class Base(object):
    def __init__(self):
        self.vk = 'vk1'

class A(Base):
    __slots__ = ['name', 'age']
    def __init__(self, name, age):
        super().__init__()
        self.name = name
        self.age = age


a = A('job', 22)

print('dir(a): ', dir(a))
print('a.__dict__: ', a.__dict__)
```

Out: 只在子类上定义`__slots__`, 实例中存在`__weakref__`方法, 并且创建的实例依然可以访问 **dict** 属性

```
dir(a):  ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__slots__', '__str__', '__subclasshook__', '__weakref__', 'age', 'name', 'vk']
a.__dict__:  {'vk': 'vk1'}
```

父类也定义`__slots__`属性后

```
class Base(object):
    __slots__ = ['vk']
    def __init__(self):
        self.vk = 'vk1'

class A(Base):
    __slots__ = ['name', 'age']
    def __init__(self, name, age):
        super().__init__()
        self.name = name
        self.age = age


a = A('job', 22)

print('dir(a): ', dir(a))
print('a.__dict__: ', a.__dict__)
```

Out: 实例中不存在`__weakref__`方法和`__dict__`方法

```
dir(a):  ['__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__slots__', '__str__', '__subclasshook__', 'age', 'name', 'vk']
Traceback (most recent call last):
  File "E:/project/demo/test/class3.py", line 20, in <module>
    print('a.__dict__: ', a.__dict__)
AttributeError: 'A' object has no attribute '__dict__'
```

在`__slots__`中添加`__weakref__`

```
from weakref import ref


class Base(object):
    __slots__ = ['vk', '__weakref__']

    def __init__(self):
        self.vk = 'vk1'


b = Base()

print('dir(b): ', dir(b))
print(ref(b))
```

Out:

```
dir(b):  ['__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__slots__', '__str__', '__subclasshook__', '__weakref__', 'vk']
<weakref at 0x0000000002BA1CC8; to 'Base' at 0x0000000002B65F98>
```


