# Python

人生苦短，我用Python（3）. 

## 数据类型

### 字典

注意一切`hashable`的类型均可为dict key, 包括`None`也可为dict key, 但`list`不可为dict key。

不合法：

* `dic = { ['a', 'b']: 1, 'c': 2,}`
* ```
tup = (1, 2, ['a', 'b']);
dic = {tup: 'value'}
```

合法：

* `dic = { ('a', 'b'): 1, 'c': 2, }` # Tuples are immutable and hashable.
* ```
tup = (1, 2, ('a', 'b'));
dic = {tup: 'value'}
```

### TODO
  * 装饰器
  * 实例方法、类方法和静态方法 3.6


### 简化代码的方式

  - 三元表达式
    ```
    return {} if return_json else ''
    ```
  - 用 if return 结束部分条件，涉及函数内有多个 return
  - 条件判断转函数

### Python 字符串前 u r b 含义

**u unicode**

表示字符串使用unicode编码。

`string = u"Python学习"`

**r raw**

表示不要转义字符串内容。

**b bytes**

表示bytes

  * python3.x里默认的str是(py2.x里的)unicode, bytes是(py2.x)的str, b”“前缀代表的就是bytes 

  * python2.x里, b前缀没什么具体意义， 只是为了兼容python3.x的这种写法

[http://blog.csdn.net/u010496169/article/details/70045895](http://blog.csdn.net/u010496169/article/details/70045895)

## 与Python2的区别
### 显式继承
  * 新式类
  * 经典类

## 打包工具

[Nuitka](https://github.com/Nuitka/Nuitka) 是一个 Python 编译器，它将 Python 代码转换为 C 代码并编译为可执行文件。实现对Python项目的打包和加密。并在无Python 环境的设备上使用。