# 单例模式

## 使用\_\_new\_\_方法

```
class Singleton(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, '_instance'):
            origin = super(Singleton, cls)
            cls._instance = origin.__new__(cls, *args, **kwargs)
        return cls._instance

class Myclass(Singleton):
    pass

a = Myclass()
b = Myclass()
print(id(a), id(b))
```

## 共享属性

```
# 创建实例时把所有实例的__dict__指向同一个字典,这样它们具有相同的属性和方法.

class Borg(object):
    _state = {}
    def __new__(cls, *args, **kw):
        ob = super(Borg, cls).__new__(cls, *args, **kw)
        ob.__dict__ = cls._state
        return ob

class MyClass2(Borg):
    a = 1
```

## 装饰器版本

```
def singleton(cls, *args, **kw):
    instances = {}
    def getinstance():
        if cls not in instances:
            instances[cls] = cls(*args, **kw)
        return instances[cls]
    return getinstance

@singleton
class MyClass:
  ...
```

## import 方法

```
# 作为python的模块是天然的单例模式

# mysingleton.py
class My_Singleton(object):
    def foo(self):
        pass

my_singleton = My_Singleton()

# to use
from mysingleton import my_singleton

my_singleton.foo()
```

## 元类实现\(魔幻\)

```
class Singleton(type):

    def __init__(cls, name, bases, attrs):
        super(Singleton, cls).__init__(name, bases, attrs)
        cls._instance = None

    def __call__(cls, *args, **kwargs):
        if cls._instance is None:
            # 以下不要使用'cls._instance = cls(*args, **kwargs)', 防止死循环,
            # cls的调用行为已经被当前'__call__'协议拦截了
            # 使用super(Singleton, cls).__call__来生成cls的实例
            cls._instance = super(Singleton, cls).__call__(*args, **kwargs)
        return cls._instance


class MyClass(metaclass=Singleton): #单例类
    # __metaclass__ = Singleton
    pass
```



