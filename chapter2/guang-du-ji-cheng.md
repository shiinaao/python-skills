Python3 中多继承按广度查找进行继承, 调用继承方法时也是如此

方法按照广度查找, 直到方法不再调用继承方法时, 按照查找的顺序逆序执行

```
class Base(object):
    def __init__(self):
        print('Base')

    def ok(self):
        print('Base-ok')

class A(Base):
    def __init__(self):
        super().__init__()
        print('A')

    def ok(self):
        super().ok()
        print('A-ok')

class B(Base):
    def __init__(self):
        super().__init__()
        print('B')

    def ok(self):
        print('B-ok')

class C(Base):
    def __init__(self):
        super().__init__()
        print('C')

class F(C, A, B):
    def __init__(self):
        super().__init__()
        print('F')

f = F()
f.ok()

# 继承关系
#    Base
#    / | \
#   C  A  B
#    \ | /
#      F

# 执行结果
# H:\Python\Python35\python.exe E:/project/py_code/base_syntax/class/class001.py
# Base
# B
# A
# C
# F
# B-ok
# A-ok
```

实例化顺序: Base -&gt; B -&gt; A -&gt; C -&gt; F

调用ok\(\)函数时的执行顺序:

按照广度查找顺序\( F -&gt; C -&gt; A -&gt; B -&gt; Base \)查找到 A, **A 调用`super().ok()` , 然后继续查找到 B.ok\(\)  
说明: 子类按照广度查找顺序调用父类方法时, 如果子类继承的父类方法中又一次调用`super()` , 则从此处开始一次独立的广度继承调用**

然后按照查找到的顺序逆序执行, 先打印`B-ok` 然后打印`A-ok`

