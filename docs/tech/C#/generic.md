# 泛型 Generic

泛型可以先不指定函数元素的数据类型，直到被编译的时候。换句话说，泛型可以编写一个不指定类型的通用的类或方法。

比如定义这样一个函数：

```c#
public T[] Reverse<T>(T[] array)
{
    var result = new T[array.Length];
    int j=0;
    for(int i=array.Length - 1; i>= 0; i--)
    {
        result[j] = array[i];
        j++;
    }
    return result;
}
```

此时没有指定传入类型，换句话说，这个函数可以接受任何类型的数组，并且返回一个相同类型的数组。

使用时：

```c#
string[] array = new string[] { "1", "2", "3", "4", "5" };
var result = reverse(array);
```

此时相当于是`public string[] Reverse(string[] array)`。


ref: 
* https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-type-parameters
* https://stackoverflow.com/a/9857185/3886059