# 枚举 Enum

枚举[默认是**int**类型](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/enum)，可以通过指定类型来改变，但必须是**整形**，比如：

```c#
enum ShoppingList : ulong
{
    Apple,
    Orange,
    Banana
}
```

## 用法

### 查看值是否在 Enum 中

C#的枚举在转换时默认不检查值是否已经在枚举中定义，即使是未定义的值也可以转换成枚举类型，但不会匹配到枚举值。

[Enum.IsDefined](https://docs.microsoft.com/en-us/dotnet/api/system.enum.isdefined?view=net-6.0) 方法可以检查值是否在枚举中定义。

eg:

```c#
public enum Waypoints
{
    A,
    B,
    C
}

Enum.IsDefined(typeof(Waypoints), 3); // False
```

ref: [Large flags enumerations in C# - Stack Overflow](https://stackoverflow.com/a/54901506/3886059)

## 位标志 Bit Flags

使用一个整形不不同比特位来做为一组开关。 例如用这个枚举来表示一个选手的多种牌型：

```c#
[Flags]
enum CardDeckSettings : uint
{
    SingleDeck = 0x01,
    LargePictures = 0x02,
    FancyNumbers = 0x04,
    Shuffle = 0x08,
}
```

需要创建枚举时，可以使用逻辑运算符 OR 来添加所需要的多个值，例如选手同时包括 SingleDeck 和 LargePictures：

```c#
CardDeckSettings settings = CardDeckSettings.SingleDeck | CardDeckSettings.LargePictures;
```

当使用条件语句判断 Flags 枚举值，注意不能使用`==`，而应该使用`HasFlag`。

查找时，可以通过 HasFlag 来检查是否包含某个值，例如：

```c#
bool IsSingleDeck = settings.HasFlag(CardDeckSettings.SingleDeck);
Console.WriteLine("Your deck is {0} which has Single Deck is {1}", settings.ToString(), IsSingleDeck);
```

输出：Your deck is 3 which has Single Deck is True

另一种方法是通过逻辑与`&`来检查是否包含某个值，例如：

```c#
bool IsSingleDeckAlternative = (settings & CardDeckSettings.SingleDeck) == CardDeckSettings.SingleDeck;
```

### Flags 特性

将枚举做为位标志时，在枚举类型前加上`[Flags]`可以告诉编译器位标志的特性，例如可以提供更多的格式化信息：

不加 Flags 特性的枚举：

```c#
enum CardDeckSettings
{
    SingleDeck = 0x01,
    LargePictures = 0x02,
    FancyNumbers = 0x04,
    Shuffle = 0x08,
}
```

```
Console.WriteLine("Your deck is {0} ", settings.ToString());
```

输出：Your deck is 3

添加 Flags 特性的枚举：

```c#
[Flags]
enum CardDeckSettings
{
    SingleDeck = 0x01,
    LargePictures = 0x02,
    FancyNumbers = 0x04,
    Shuffle = 0x08,
}

...

Console.WriteLine("Your deck is {0} ", settings.ToString());
```

输出：Your deck is SingleDeck, LargePictures

### 扩展方法

#### 判断是否包含某个值

对于 Flags 枚举，可以通过扩展方法来判断是否包含某个值，例如：

```c#
/// <summary>
/// 获取枚举值的所持有的标志位
/// Retrieves all individual flag values contained in a Flag type enumeration.
/// </summary>
/// <param name="value">枚举值</param>
/// <typeparam name="T">Flag类型</typeparam>
/// <returns>所有元素的集合</returns>
public static IEnumerable<T> GetValues<T>(this T value) where T : Enum
{
    return Enum.GetValues(value.GetType()).Cast<T>().Where(v => value.HasFlag(v));
}
```

#### 配合 switch 语句使用

如果想要配合 switch 语句使用，实现只命中 Flags 值中的第一个判断时，可以使用 C# 7 引入的 [switch pattern matching](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/functional/pattern-matching)：

```c#
CardDeckSettings settings = CardDeckSettings.SingleDeck | CardDeckSettings.LargePictures;

switch(settings)
{
    case var _ when settings.HasFlag(CardDeckSettings.SingleDeck):
        Console.WriteLine("Single Deck");
        break;
    case var _ when settings.HasFlag(CardDeckSettings.LargePictures):
        Console.WriteLine("Large Pictures");
        break;
    case var _ when settings.HasFlag(CardDeckSettings.FancyNumbers):
        Console.WriteLine("Fancy Numbers");
        break;
    case var _ when settings.HasFlag(CardDeckSettings.Shuffle):
        Console.WriteLine("Shuffle");
        break;
}
// 输出：Single Deck
```

如果想要命中所有的 Flags 值，最简单的方法是做 if 判断：

```c#
if(settings.HasFlag(CardDeckSettings.SingleDeck)) Console.WriteLine("Single Deck");
if(settings.HasFlag(CardDeckSettings.LargePictures)) Console.WriteLine("Large Pictures");
if(settings.HasFlag(CardDeckSettings.FancyNumbers)) Console.WriteLine("Fancy Numbers");
if(settings.HasFlag(CardDeckSettings.Shuffle)) Console.WriteLine("Shuffle");
// 输出：Single Deck
// 输出：Large Pictures
```

ref:

- [C# 7.0 Pattern Matching](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-7#pattern-matching)
- [c# - Switch on Enum (with Flags attribute) without declaring every possible combination? - Stack Overflow](https://stackoverflow.com/a/52290348)

### 注意事项

对于大量的枚举值，当超过默认`uint`所代表的 32 位范围后，可以使用`ulong`来代替，注意将 1 替换为 1UL，比如：

```c#
[Flags]
    public enum EventType : ulong
    {
        f1= 1,
        f2= 1 << 1,
        f3= 1 << 2,
        ......

        f... = 1 << 30,
        f... = 1UL << 31,
        f...  = 1UL << 32
    }
```
