# C语言

## 类型转换

### 强制类型转换
```
(Type)value;
```
程序员控制

### 隐式类型转换
```
char c = 0;
short s = c;
int i = s;
long l = i;
```
编译器主动发生，注意类型从低到高转换安全。

[[https://www.cnblogs.com/solidblog/p/3381628.html|C++隐式类型转换]]


## if语句

### 布尔类型比较时直接写在条件中

```
// 表示为真
if (m_bool)
{
    // 语句
}

// 表示为假
if (!m_bool)
{
    // 语句
}
```
[[https://blog.csdn.net/mitu405687908/article/details/51085605|常见变量与零值比较]]

### 与常量比较时常量写在左边

防止漏写一个等号后通过编译

[[https://blog.csdn.net/mitu405687908/article/details/51085605|常见变量与零值比较]]

### 与浮点型比较时注意先定义精度

[[https://www.cnblogs.com/youxin/p/3306136.html|float 浮点数与零值0比较大小 - youxin - 博客园]]

## 结构体

空结构体的大小

```
#include<stdio.h>

int main(void){
    struct TS{

    };
    printf("%ld\n",sizeof(struct TS));

    return 0;
}
```
空结构体的内存占用为0

## sizeof是C语言关键字，不是函数

```
#include<stdio.h>
int main(void){
    int var = 0;
    int size = sizeof(var++);

    printf("var = %d, size = %d\n", var, size);

    return 0;
}
```

## 布尔类型

需要加入头文件 `stdbool.h`:

```
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

int main(void) {
    bool keep_going = true;  //也可以是`bool keep_going = 1;`
    while(keep_going) {
        printf("本程序会在keep_going为真时持续运行。\n");
        keep_going = false;    // 也可以是`keep_going = 0;`
    }
    printf("停止运行！\n");
    return EXIT_SUCCESS;
}
```
[[https://zh.wikipedia.org/wiki/Stdbool.h|stdbool.h - 维基百科，自由的百科全书]]

### 三目运算符

三目运算符中如果要执行多条语句需要用小括号包裹，用逗号隔开：

```
strcmp(input_dict[c], LastInput)==0 ? 1 : (strcpy(dict[j], input_dict[c]), j++);
```

true 表示Pass,小括号内包括多条语句。

### gdb 打印二维数组

```
p ((int (*)[6]) dmap)[1]
```