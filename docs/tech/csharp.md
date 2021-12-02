# C Sharp

Visual Studio 编译器 `csc`。

WPF是 C#的 GUI 编写技术，使用 XAML 编写界面。

编译发布： `dotnet publish -c Release -r win10-x64`

## 类

字段是类里面的变量。

与C和cpp不同，c#在类型的外部不能声明全局变量（也就是变量或字段）。所有的**字段都属于类型**，而且必须在类型声明内部声明。
同样的，c#中**没有全局函数（也就是方法或函数）**声明在类型声明的外部。

### 访问修饰符：

指定成员的访问级别。

* private (默认)，只有类内部可访问。
* public 可以被其他对象访问。
* protected 只有类内部和类派生出的子类可以访问。
* internal 只有程序集内的类可以访问。
* protected internal == protected + internal 派生出的子类和程序集内的类可以访问。

抽象成员

## 框架

* web framework: [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
* backend framework: [Entity](https://docs.microsoft.com/en-us/ef/core/)