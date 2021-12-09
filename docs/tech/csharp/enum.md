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

