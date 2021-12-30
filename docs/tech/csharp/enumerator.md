# 枚举器 Enumerator

数组、列表等都是可被枚举的数据类型，都有枚举器。

获取对象枚举器的方法是GetEnumerator()，方法返回一个枚举器。

枚举器包含三个成员，分别是Current、MoveNext()和Reset()。

Current：返回当前枚举器的值。

MoveNext：移动到下一个值，返回值是Boolean，指示新的位置是有效的，还是已经到达了序列的底部。

**枚举器的初始位置在第一个元素之前，所以在第一次使用Current之前必须前MoveNext一次**

Reset：重置枚举器，将枚举器移动到第一个元素之前。

```c#
static void Main()
{
    // Creates and initializes a new Array.
    String[] myArr = new String[10];
    myArr[0] = "The";
    myArr[1] = "quick";
    myArr[2] = "brown";
    myArr[3] = "fox";
    myArr[4] = "jumps";
    myArr[5] = "over";
    myArr[6] = "the";
    myArr[7] = "lazy";
    myArr[8] = "dog";

    // Displays the values of the Array.
    int i = 0;
    System.Collections.IEnumerator myEnumerator = myArr.GetEnumerator();
    Console.WriteLine("The Array contains the following values:");
    while ((myEnumerator.MoveNext()) && (myEnumerator.Current != null))
        Console.WriteLine("[{0}] {1}", i++, myEnumerator.Current);
    // reset the enumerator
    myEnumerator.Reset();
    // remember the initial position is before the 1st item in the sequence
    // movenext before use
    myEnumerator.MoveNext();
    Console.WriteLine("Ready to iterate again, now on {0}", myEnumerator.Current);
}
```


## 泛型枚举

泛型版本的枚举为 `IEnumerable<T>`，泛型枚举不需要object基类的引用，而且类型安全，而非泛型枚举不具备这两个条件。

