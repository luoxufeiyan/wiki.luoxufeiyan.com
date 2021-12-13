# C#

Visual Studio 编译器 `csc`。

WPF是 C#的 GUI 编写技术，使用 XAML 编写界面。

编译发布： `dotnet publish -c Release -r win10-x64`


## 小抄速记

快速对数组初始化同一个值： `byte[] arr1 = Enumerable.Repeat((byte)0x20,100).ToArray();` [ref](https://stackoverflow.com/questions/6150097/initialize-a-byte-array-to-a-certain-value-other-than-the-default-null)

## 框架

* web framework: [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
* backend framework: [Entity](https://docs.microsoft.com/en-us/ef/core/)