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

## 小抄速记

快速对数组初始化同一个值： `byte[] arr1 = Enumerable.Repeat((byte)0x20,100).ToArray();` [ref](https://stackoverflow.com/questions/6150097/initialize-a-byte-array-to-a-certain-value-other-than-the-default-null)

## 框架

* web framework: [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
* backend framework: [Entity](https://docs.microsoft.com/en-us/ef/core/)