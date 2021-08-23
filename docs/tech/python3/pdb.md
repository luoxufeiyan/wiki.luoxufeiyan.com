# pdb调试工具

pdb是python自带的调试工具包。

N next单步运行
S 单步运行，进入函数。
C continue 继续

B breakpoint 断点
p  打印变量值。

```
import pdb
pdb.set_trace()
```

## 遇到错误时进入pdb

```
python3 -m pdb -c continue filename.py
```
https://stackoverflow.com/questions/242485/starting-python-debugger-automatically-on-error/2438834#2438834