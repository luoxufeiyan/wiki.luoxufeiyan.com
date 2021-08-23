# 数组

需要`string.h`头文件

初始化
```
int a[10];
memset(a, 0, sizeof(a));
```

数组赋值
```
int a[10];
int b[10];
memcpy(b, a, sizeof(a));
```

# 二维数组

列数必须指定
```
int arr[][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}; 
```

## 传参数为二维数组
[[https://www.geeksforgeeks.org/pass-2d-array-parameter-c/|How to pass a 2D array as a parameter in C?]]