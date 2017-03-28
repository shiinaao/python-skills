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



