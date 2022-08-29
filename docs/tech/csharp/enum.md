# 枚举 Enum

枚举默认是int类型，可以通过指定类型来改变，但必须是**整形**，比如：
```c#
enum ShoppingList : ulong
{
    Apple,
    Orange,
    Banana
}
```

## 位标志 Bit Flags

使用一个整形不不同比特位来做为一组开关。 例如用这个枚举来表示一个选手的多种牌型：

```c#
enum CardDeckSettings : uint
{
    SingleDeck = 0x01,
    LargePictures = 0x02,
    FancyNumbers = 0x04,
    Shuffle = 0x08,
}
```

需要创建枚举时，可以使用逻辑运算符OR来添加所需要的多个值，例如选手同时包括SingleDeck和LargePictures：

```c#
CardDeckSettings settings = CardDeckSettings.SingleDeck | CardDeckSettings.LargePictures;
```

查找时，可以通过HasFlag来检查是否包含某个值，例如：

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

不加Flags特性的枚举：

```c#
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

输出：Your deck is 3

添加Flags特性的枚举：

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

对于大量的枚举值，当超过默认`uint`所代表的32位范围后，可以使用`ulong`来代替，注意将 1 替换为 1UL，比如：

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

### 查看值是否在Enum中

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