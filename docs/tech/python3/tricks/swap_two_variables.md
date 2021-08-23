# 不借助中间变量交换两个变量的值
使用a,b=b,a而不是c=a;a=b;b=c;来交换a,b的值，可以快1倍以上。
```
In [3]: %%timeit –n 10000
    a,b=1,2
   ….: c=a;a=b;b=c;
   ….:
10000 loops, best of 3: 172 ns per loop
In [4]: %%timeit –n 10000
a,b=1,2
a,b=b,a
   ….:
10000 loops, best of 3: 86 ns per loop
```