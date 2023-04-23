# 集合 Collections

## 索引与范围

### Range 范围

C# 8中引入了新的范围运算符`x..y`，可以用来指定范围。

```c#
int[] arr = Enumerable.Range(1,10).ToArray();
Console.WriteLine(string.Join(" ,", arr)); //1 ,2 ,3 ,4 ,5 ,6 ,7 ,8 ,9 ,10
Console.WriteLine(string.Join(" ,", arr[2..])); //3 ,4 ,5 ,6 ,7 ,8 ,9 ,10
Console.WriteLine(string.Join(" ,", arr[..2])); //1 ,2
Console.WriteLine(string.Join(" ,", arr[1..3])); //2 ,3
Console.WriteLine(string.Join(" ,", arr[..])); //1 ,2 ,3 ,4 ,5 ,6 ,7 ,8 ,9 ,10 全部元素，跟 arr 一样 
```

注意这里取值的区间是**前闭后开[x,y)**区间，后面的值是取不到的。

例如 `Console.WriteLine(string.Join(" ,", arr[1..3])); //2 ,3` 这里取不到索引 3 上的元素 4 。

#### index from end operator 从尾索引

从最后的元素开始索引的运算符`^`，代表用列表长度减去运算符后面的值，例如`^1`表示`列表长度 - 1`，代表最后一个元素。

```c#
int[] arr = Enumerable.Range(1,10).ToArray();
Console.WriteLine(arr[^1]); //10
Console.WriteLine(arr[^2]); //9
Console.WriteLine(arr[^0]); //Error: System.IndexOutOfRangeException
```

## Span

**WIP**

C# 7中引入的Span数据类型，可以对集合内的元素使用`Slice`方法进行切片。

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