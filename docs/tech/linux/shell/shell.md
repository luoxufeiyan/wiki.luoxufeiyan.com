# Shell 学习

## 变量

**重要!** Shell变量赋值时**不能**有空格，必须在等号前后紧挨着写内容。

定义时不用美元符，调用时需要用美元符。

```
a=10
echo $a
```



### 数组

**重要!** 定义数组时用**空格**分隔，不是逗号。

```
a=(19 23 53 22)
```

### 变量自增

使用双括号或者`expr`进行赋值运算。

```
num=$((num + 1))
num=$(expr $num + 1)
```

## 文件读入

### 读取键盘输入到变量

`read`读取从键盘的输入，并赋给其后的变量。

```
read ipt
echo "Your input is:" $ipt
```

```
num=`expr "$num" + 1`
```

### 按行读入文件

```
while read line; do
    echo $line;
done < filename.txt
```

### 按扩展名读入文件

```
for file in *.sh;do
    echo "Found a shell script named:" $file
done
```

## 管道

保存输出文件`cat << EOF > gcc.sh`

```
gao@xm1:~/Documents/assn/2$ cat << EOF > gcc.sh
> #!/bin/dash
> for c_file in *.c
> do
>     gcc -c $c_file
> done
> EOF
gao@xm1:~/Documents/assn/2$ cat gcc.sh 
#!/bin/dash
for c_file in *.c
do
    gcc -c 
done
```

## 输出重定向

将`stdout`和`stderr`隐藏。

```
COMMAND > /dev/null 2>&1
```
[bash script - redirecting to /dev/null - Unix &amp; Linux Stack Exchange](https://unix.stackexchange.com/questions/119648/redirecting-to-dev-null)

## IFS

bash内部的文件分隔符。

[详细解析Shell中的IFS变量_洛奇看世界-CSDN博客_bash ifs](https://blog.csdn.net/guyongqiangx/article/details/80220434)

## 流程控制

### for循环

可以使用`for i in $(seq 10);`以及类似C语言的两种写法。

类似C语言式，注意为两层小括号包裹`((i=0;i<10;i++))`：
```
for ((i=0;i<10;i++)); do
    echo "Foo"
done
```

Shell式：
```
for i in $(seq 10); do
    echo "Yoo"
done
```

循环列表内的全部元素：
```
a=(19 23 53 22)

for num in "${a[@]}"; do
    echo "Here is an element $num"
done
```

注意写for循环时**必须**有双引号包裹，`"${a[@]}"`，否则当数组内元素有空格时，循环会中断。

## 常用命令

### 比较文件不同

`diff` 输出两文件的不同。

```
(base) ➜  playground cat 1.txt 
Hihihihihi
(base) ➜  playground cat 2.txt 
Hihihihihi
Nihao
(base) ➜  playground diff 1.txt 2.txt 
1a2
> Nihao
(base) ➜  playground echo $?
1

```

文件不同会返回`1`，`$？`为1。

### 生成随机token


```
dd if=/dev/urandom  count=1 bs=128 | sha1sum
```

### tr命令

转换特定字符，`tr '0123456789' '<<<<<5>>>>'`将01234转为<，将6789转为>，5保持不变。

```
(base) ➜  playground tr '0123456789' '<<<<<5>>>>'
12839
<<><>
2137895769832
<<<>>>5>>>><<
3123213
<<<<<<<
```

### cut命令

按照特定分隔符来分割，只支持单个字符。

`-d` 为分割标志，默认为tab。

`-f` 为显示段落，`-f 2`为显示第二段，`-f 2-`为显示第二段及以后。

```
(base) ➜  playground echo 123,456,abc,def|cut -d',' -f 2 
456
```

### test命令

测试语句是否为真。

字符串比较用`= !=`

数字比较用`-eq -ne -lt -gt`



`test "$msg" = "Foobar"`



测试文件：



`-e` 文件存在则为真

`-d` 为目录则为真

`-a` 逻辑And，`-o`逻辑Or，`test $a -gt 10 -a -lt 15`

## 扩展阅读

[Shell+Regex 复习笔记（9044） - 知乎](https://zhuanlan.zhihu.com/p/189612731)