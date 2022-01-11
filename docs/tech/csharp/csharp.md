# C#

Visual Studio 编译器 `csc`。

WPF是 C#的 GUI 编写技术，使用 XAML 编写界面。

编译发布： `dotnet publish -c Release -r win10-x64`


## 空安全 null safety

c# 支持 空判断 `??` 运算符，当运算符左侧为null时，执行运算符右侧的代码。

```c#
double SumNumbers(List<double[]> setsOfNumbers, int indexOfSetToSum)
{
    return setsOfNumbers?[indexOfSetToSum]?.Sum() ?? double.NaN;
}

var sum = SumNumbers(null, 0);
Console.WriteLine(sum);  // output: NaN
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

因为String类型是不可变的，所以在每次操作后，都需要分配新的内存。对于一些需要频繁修改的字符串，String的内存开销非常大，可以使用StringBuilder类来提高性能。

StringBuilder可以修改字符串而不创建新的对象。

创建时可以指定初始容量，如果不指定，则默认为16。

```c#
StringBuilder myStringBuilder = new StringBuilder("Hello World!");
StringBuilder myStringBuilder2 = new StringBuilder("Hello World!", 20);
StringBuilder myStringBuilder3 = new StringBuilder(20);
```

ref:

* https://docs.microsoft.com/en-us/dotnet/standard/base-types/stringbuilder
* https://blog.csdn.net/PEACE_FOREVER_1996/article/details/77726957


## class vs struct

类与结构体的不同。


|Class|Struct |
|--|--|
|Reference types (on heap)  |value types (on stack) |
|Can have constructor and destructor| No constructor destructor|
|can have null type|cannot have null type|

ref:

* https://stackoverflow.com/questions/13049/whats-the-difference-between-struct-and-class-in-net

## XML 注释语法

c# 使用XML注释语法，以 `///` 开头。

### <inheritdoc>

对于继承的类(override)，可以使用 `<inheritdoc>` 来自动生成跟父类一样的文档。

```c#
/// <inheritdoc />
public override int CourseType { set; get; } = 12;
```

ref:
* https://tunnelvisionlabs.github.io/SHFB/docs-master/SandcastleBuilder/html/79897974-ffc9-4b84-91a5-e50c66a0221d.htm
* https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/xmldoc/recommended-tags#inheritdoc
## 小抄速记

快速对数组初始化同一个值： `byte[] arr1 = Enumerable.Repeat((byte)0x20,100).ToArray();` [ref](https://stackoverflow.com/questions/6150097/initialize-a-byte-array-to-a-certain-value-other-than-the-default-null)

## 框架

* web framework: [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
* backend framework: [Entity](https://docs.microsoft.com/en-us/ef/core/)