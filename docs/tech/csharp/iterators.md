# Iterators

迭代器块产生了枚举器。

```c#
class MyClass
{
    public IEnumerator<string> GetEnumerator()
    {
        return BlackAndWhite(); //枚举器
    }

    public IEnumerator<string> BlackAndWhite()
    {
        yield return "black";
        yield return "gray";
        yield return "white";
    }
}
public class Program
{
    static void Main()
    {
        MyClass mc = new MyClass();
        foreach (string shade in mc)
        {
            Console.WriteLine(shade);
        }
    }
}
```

迭代器产生可枚举类型。

```c#
class MyClass
{
    public IEnumerator<string> GetEnumerator()
    {
        IEnumerable<string> myEnumerable = BlackAndWhite(); //可枚举类型
        return myEnumerable.GetEnumerator(); //枚举器
    }

    public IEnumerable<string> BlackAndWhite()
    {
        yield return "black";
        yield return "gray";
        yield return "white";
    }
}

class Program
{
    static void Main()
    {
        MyClass mc = new MyClass();

        foreach (string shade in mc)
        {
            Console.Write("{0} ", shade);
        }
    }
}
```