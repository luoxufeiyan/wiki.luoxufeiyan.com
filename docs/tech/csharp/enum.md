# enum

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