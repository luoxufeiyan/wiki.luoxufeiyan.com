# 接口 Interface

接口是一组函数成员，但不实现他们。

接口可以解决类型的兼容性问题，将类型提取出一套统一的格式以供其他程序使用。

例如 CA 和 CB 类含有不同格式的个人信息，接口就可以很方便的把个人信息提取出来，以便其他程序使用。

```c#
interface IInfo //定义接口
{
    string GetName();
    string GetAge();
}

class CA : IInfo // 声明CA类实现了这个接口
{
    public string Name;
    public int Age;

    // 实现接口
    public string GetName() => Name;
    public string GetAge() => Age.ToString();
}

class CB : IInfo
{
    public string FirstName;
    public string LastName;
    public int Age;

    public string GetName() => FirstName + " " + LastName;
    public string GetAge() => Age.ToString();
}

class Program
{
    static void PrintPersonalInfo(IInfo item) // 传入接口引用
    {
        Console.WriteLine($"Name: {item.GetName()}, Age: {item.GetAge()}");
    }

    static void Main()
    {
        CA ca = new CA() { Name = "Carson", Age = 18 };
        CB cb = new CB() { FirstName = "Jack", LastName = "Li", Age = 20 };

        PrintPersonalInfo(ca);
        PrintPersonalInfo(cb);
    }
}
```

可以扩展BCL基础库中实现的接口，来实现自定义的功能，例如自定义类型MyClass希望实现Array.Sort方法，可以通过扩展 `ICompareable` 接口来实现对应的比较方法。

```c#
class MyClass : IComparable
{
    public int TheValue;
    public int CompareTo(object? obj) // CompareTo是接口里声明的比较方法
    {
        MyClass mc = (MyClass) obj;
        if (this.TheValue < mc.TheValue) return -1;
        if (this.TheValue > mc.TheValue) return 1;
        return 0;
    }
}
```

这样可以实现Array.Sort()方法：

```c#
MyClass[] myArr = new MyClass[5];
Array.Sort(myArr);
```

## 声明接口

除了实现BCL中的接口外，也可以自己声明接口。

但声明接口不能包括数据成员或者静态成员。

