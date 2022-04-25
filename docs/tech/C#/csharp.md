# C#

Visual Studio 编译器 `csc`。

WPF 是 C#的 GUI 编写技术，使用 XAML 编写界面。

编译发布： `dotnet publish -c Release -r win10-x64`

## 空安全 null safety

c# 支持 空判断 `??` 运算符，当运算符左侧为 null 时，执行运算符右侧的代码。

```c#
double SumNumbers(List<double[]> setsOfNumbers, int indexOfSetToSum)
{
    return setsOfNumbers?[indexOfSetToSum]?.Sum() ?? double.NaN;
}

var sum = SumNumbers(null, 0);
Console.WriteLine(sum);  // output: NaN
```

`??=` 运算符当左侧为 null 时，赋值右侧的值。

```c#
List<int> numbers = null;
int? a = null;

(numbers ??= new List<int>()).Add(5);
Console.WriteLine(string.Join(" ", numbers));  // output: 5

numbers.Add(a ??= 0);
Console.WriteLine(string.Join(" ", numbers));  // output: 5 0
Console.WriteLine(a);  // output: 0
```

ref: [?? and ??= operators - C# reference | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator)

## Span

```c#
static void Main()
{
    var array = new byte[10];
    Span<byte> bytes = array;
    bytes = bytes.Slice(start: 2, length: 5);

    bytes[0] = 5;
    Console.WriteLine(array[2]);
    Console.WriteLine(bytes[0]);
}
```

## StringBuilder

因为 String 类型是不可变的，所以在每次操作后，都需要分配新的内存。对于一些需要频繁修改的字符串，String 的内存开销非常大，可以使用 StringBuilder 类来提高性能。

StringBuilder 可以修改字符串而不创建新的对象。

创建时可以指定初始容量，如果不指定，则默认为 16。

```c#
StringBuilder myStringBuilder = new StringBuilder("Hello World!");
StringBuilder myStringBuilder2 = new StringBuilder("Hello World!", 20);
StringBuilder myStringBuilder3 = new StringBuilder(20);
```

ref:

- https://docs.microsoft.com/en-us/dotnet/standard/base-types/stringbuilder
- https://blog.csdn.net/PEACE_FOREVER_1996/article/details/77726957

## class vs struct

类与结构体的不同。

| Class                               | Struct                    |
| ----------------------------------- | ------------------------- |
| Reference types (on heap)           | value types (on stack)    |
| Can have constructor and destructor | No constructor destructor |
| can have null type                  | cannot have null type     |

ref:

- https://stackoverflow.com/questions/13049/whats-the-difference-between-struct-and-class-in-net

## XML 注释语法

c# 使用 XML 注释语法，以 `///` 开头。

### <inheritdoc>

对于继承的类(override)，可以使用 `<inheritdoc>` 来自动生成跟父类一样的文档。

```c#
/// <inheritdoc />
public override int CourseType { set; get; } = 12;
```

ref:

- https://tunnelvisionlabs.github.io/SHFB/docs-master/SandcastleBuilder/html/79897974-ffc9-4b84-91a5-e50c66a0221d.htm
- https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/xmldoc/recommended-tags#inheritdoc

### ref

> 在C#中，方法的参数传递有四种类型：传值（by value），传址（by reference），输出参数（by output），数组参数（by array）。
> 传值参数无需额外的修饰符，传址参数需要修饰符ref，输出参数需要修饰符out，数组参数需要修饰符params。
> 传值参数在方法调用过程中如果改变了参数的值，那么传入方法的参数在方法调用完成以后并不因此而改变，而是保留原来传入时的值。
> 传址参数恰恰相反，如果方法调用过程改变了参数的值，那么传入方法的参数在调用完成以后也随之改变。
> 实际上从名称上我们可以清楚地看出两者的含义--传值参数传递的是调用参数的一份拷贝，而传址参数传递的是调用参数的内存地址，该参数在方法内外指向的是同一个存储位置。


带 ref 的参数会在方法执行完后改变参数的值(因为传递的是地址)。

例：

```c#
static void Test()
{
    string s1 = "Good Luck!";
    TestRef(ref s1);
    Console.WriteLine(s1);//output: Hello World!
}

static void TestRef(ref string str)
{
    str = "Hello World!";
}
```

**传递到 ref 参数的参数必须初始化,否则程序会报错**

因为 ref 实际是在传**地址**，需要初始化变量。

```c#
static void Test()
{
    string s1;
    TestRef(ref s1);
    Console.WriteLine(s1);//Use of unassigned parameter
}

static void TestRef(ref string str)
{
    str = "Hello World!";
}
```

### out 关键字

使用 out 关键字可以使参数按照引用（原变量）来传递，而不是在传入参数时创建一个参数的拷贝。

out 关键字与 ref 关键字类似，但 out 不必在调用前初始化。

```c#
static void Test()
{
    string s1;
    TestOut(out s1);
    Console.WriteLine(s1);
}

static void TestOut(out string str)
{
    str = "Hello World!";
}
```

out关键字无法将参数的值传入方法中，（只传递的是方法的引用）。在使用 out 的变量时，初始化必须要在方法的内部进行，否则程序会报错。

```c#
static void Test()
{
    string s1; // 这里赋值也会报错，需要在方法内赋值
    TestOut(out s1);
    
}

static void TestOut(out string str)
{
    Console.WriteLine(str);//Use of unassigned parameter
    str = "Hello World!";
}
```

#### 使用

利用 out 可以间接实现一个函数返回多个类型的值。

例如求最大最小值是 int 类型，平均值是 double 类型，使用 out 可以一次性返回这些值。

```c#
static readonly List<int> _arr = new List<int> { 1, 4, 2, 5, 6, 7, 9, 2, 5 };

static void Main()
{

    int min, max;
    double avg;
    CalcArr(out min, out max, out avg);
    Console.WriteLine("Min {0}, max {1}, avg {2}", min, max, avg);
}

static void CalcArr(out int min, out int max, out double avg)
{
    min = _arr.Min();
    max = _arr.Max();
    avg = _arr.Average();
}
```

## 小抄速记

快速对数组初始化同一个值： `byte[] arr1 = Enumerable.Repeat((byte)0x20,100).ToArray();` [ref](https://stackoverflow.com/questions/6150097/initialize-a-byte-array-to-a-certain-value-other-than-the-default-null)

## 框架

- web framework: [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
- backend framework: [Entity](https://docs.microsoft.com/en-us/ef/core/)

## Jupyter 交互式编程

将 C# 安装至 jupyter，实现交互式编程：[Using .NET notebooks with Jupyter Notebook / JupyterLab](https://github.com/dotnet/interactive/blob/main/docs/NotebookswithJupyter.md)

### Import package

import from NuGet: `#r "nuget:<package name>,<package version>"`

can be found in NuGet package page, under **Script & Interactive** tab.

eg:

```c#
#r "nuget: morelinq, 3.3.2"
using MoreLinq;
```

ref: https://devblogs.microsoft.com/dotnet/net-core-with-juypter-notebooks-is-here-preview-1/

## ref

- 单元测试：https://docs.microsoft.com/en-us/visualstudio/test/walkthrough-creating-and-running-unit-tests-for-managed-code?view=vs-2022
