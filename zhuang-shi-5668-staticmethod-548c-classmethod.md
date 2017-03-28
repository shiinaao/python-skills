```
class A(object):
    def foo(self,x):
        print "executing foo(%s,%s)"%(self,x)

    @classmethod
    def class_foo(cls,x):
        print "executing class_foo(%s,%s)"%(cls,x)

    @staticmethod
    def static_foo(x):
        print "executing static_foo(%s)"%x

a=A()
```

`@staticmethod` 装饰的方法会变成一个普通的函数, `A.static_foo()`和`a.static_foo()`的调用结果是一样的

`@classmethods`装饰的方法, 隐藏的传递给第一个参数的对象实体的类\(class A\)而不是self.



详细: [装饰器@staticmethod和@classmethod有什么区别?](https://taizilongxu.gitbooks.io/stackoverflow-about-python/14/README.html)

