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

# Enumerable

## Methods 

### SkipWhile

Bypasses elements in a sequence as long as a specified condition is true and then returns the remaining elements.

跳过集合中所有的条件为真的元素，（当第一次遇到条件为假时）返回剩余的元素。

例如想从 fruits 集合中分隔出 Date 及以后的水果。

```csharp
IEnumerable<string> fruits = new List<string>
{
	"Apple",
	"Banana",
	"Cherry",
	"Date",
	"Elderberry",
	"Fig"
};

fruits = fruits.SkipWhile(f => f != "Date"); // 集合中的 Date 在这个条件返回假，使 SkipWhile 生效。
Console.WriteLine(string.Join(',', fruits)); // Date,Elderberry,Fig
```

此条件只判断一次。

例如想从集合中过滤出大于等于 5 的元素，如果集合中的元素未排序，可能无法过滤。

```csharp
IEnumerable<int> b = new List<int>(){ 1, 3, 5, 6, 0, 2, 3 };
b = b.SkipWhile(e => e < 5);
Console.WriteLine(string.Join(',', b)); // 5,6,0,2,3
```

这里后面的 0 2 3 也被选中了，此方法不适用未排序的集合。



ref: [Enumerable.SkipWhile Method (System.Linq) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.skipwhile?view=net-8.0)