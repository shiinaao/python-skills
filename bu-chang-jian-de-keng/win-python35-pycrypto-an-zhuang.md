# Windows Python3.5 PyCrypto 安装

现在最流行的密码学库应该是`Cryptography` , 支持Python2.6-2.7, Python3.2+ 和 PyPy  
然而`PyCrypto` 只支持Python2.1-3.3

但是有一天我拿到了一个需要用`PyCrypto` 的脚本, 根本不懂密码学的我修改脚本失败后只好去安装一下`PyCrypto` 

```
error: Microsoft Visual C++ 14.0 is required. 
Get it with "Microsoft Visual C++ Build Tools": http://landinghub.visualstudio.com/visual-cpp-build-tools
```

看起来装一下环境也不是不能解决问题, 但是装的确实有点慢了, 然后我发现早已有人解决了这问题[**PyCrypto-Wheels**](https://github.com/sfbahr/PyCrypto-Wheels)

64-bit

```
pip install --use-wheel --no-index --find-links=https://github.com/sfbahr/PyCrypto-Wheels/raw/master/pycrypto-2.6.1-cp35-none-win_amd64.whl pycrypto
```

32-bit

```
pip install --use-wheel --no-index --find-links=https://github.com/sfbahr/PyCrypto-Wheels/raw/master/pycrypto-2.6.1-cp35-none-win32.whl pycrypto
```

一行解决问题看起来很高端, 其实只是手动安装wheels包

结局是, 即使装上了库, 脚本还是没跑起来, 反倒是需要脚本解决的问题解决了

