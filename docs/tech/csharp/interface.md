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

