# Python 基本操作

### 列表新增元素

1.
```
shopping_list = []
fruit = {"apple":3.2, "orange": 2.4, "banana": 1.7, "kiwi": 2.5}
for key in fruit:
    List.append(key)
```

### 进制转换
```
int("0101",2)   二进制==>十进制
int("0101",3)   三进制==>十进制

hex(1024)
oct(1024)
bin(1024)
```

### 列表转set可去重
```
>>> l1 = ['b','c','d','b','c','a','a']
	    
>>> l2 = set(l1)
	    
>>> l2
	    
{'c', 'a', 'd', 'b'}
```

### Counter统计元素出现个数
```
from collections import Counter

a = [10, 8, 6, 7, 2, 8, 4, 10, 3, 7, 8, 4, 5, 7, 2, 2, 3, 8, 8, 9, 6, 2, 2, 7, 8, 7, 4, 8, 5, 2]

b = Counter(a)
print(b)

Counter({8: 7, 2: 6, 7: 5, 4: 3, 10: 2, 6: 2, 3: 2, 5: 2, 9: 1})
--------------------- 
作者：geerniya 
来源：CSDN 
原文：https://blog.csdn.net/geerniya/article/details/78638457 
版权声明：本文为博主原创文章，转载请附上博文链接！
```

### 列表中的循环嵌套

```
>>> [i for i in range(4)]
	    
[0, 1, 2, 3]
```

### 函数帮助

```
>>> help(print)
	    
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.

>>> dir(print)
	    
['__call__', '__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__name__', '__ne__', '__new__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__self__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__text_signature__']

```

### 打开文件

```
with open("test.txt") as test:
    ...
```
此写法不需要f.close()

### 二维数组排序

```
lst = [['G', 10], ['A', 22], ['S', 1], ['P', 14], ['V', 13], ['T', 7], ['C', 0], ['I', 219]]


>>> sorted(lst, key=lambda x: x[1], reverse=True)
[['I', 219], ['A', 22], ['P', 14], ['V', 13], ['G', 10], ...]

```
https://stackoverflow.com/questions/20099669/python-sort-multidimensional-array-based-on-2nd-element-of-subarray


### 判断变量类型
```
>>> a = "foo"
>>> print(type(a))
<class 'str'>
>>> isinstance(a, str)
True
```

### divmod除法
```
>>> 100//3
33
>>> 100%3
1
>>> div, mod = divmod(100,3) #整数，余数
>>> print(div, mod)
33 1
```

### 字符串倒序
```
>>> s1 = "apple"
>>> s2 = "".join(reversed(s1))
>>> s2
'elppa'
```

### eval()函数
```
>>> x = 5
>>> t = 3
>>> eval(x+t)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: eval() arg 1 must be a string, bytes or code object
>>> eval("x+t")
8
```
