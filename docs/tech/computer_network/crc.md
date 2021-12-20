# CRC 校验

CRC使用**模2除法**进行计算，相当于XOR运算，不产生进位和借位。


生成多项式是CRC校验中使用到的除数，例如：

```math
g（x）= x^5 + x^3 + x^1 +1
```

表示这个二进制的第5位、第3位、第1位和第0位的二进制均为1，其它位均为0，即二进制表示为：101011。


步骤：

下面的除法均为模2除法，不产生进位和借位。

1. 首先选择一个除数，一般是用多项式表示，称为**生成多项式**，假设为k位。
2. 在需要处理的数据字段（假设为m位）后加上`k-1`位的0，然后用这个新帧去除以除数（生成多项式），余数就是该帧的CRC校验码。
3. 在数据字段后面加上CRC校验码，这样就完成了CRC校验。发送给接收方（m+k-1位）。
4. 对于接收方，将收到的数据除以除数（生成多项式），如果余数为0则校验通过。


## snippet

```python3
import zlib
hex(zlib.crc32(b'hello-world') & 0xffffffff)
```

## ref
* 推荐：[最通俗的CRC校验原理剖析](https://blog.51cto.com/winda/1063951)
* [A PAINLESS GUIDE TO CRC ERROR DETECTION ALGORITHMS](https://zlib.net/crc_v3.txt)
* [循环冗余校验（CRC）算法入门引导](https://blog.csdn.net/liyuanbhu/article/details/7882789)