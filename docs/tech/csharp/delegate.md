# 委托 Delegate

委托类似于一个面向对象的函数指针。

类表示的是数据和方法的集合，而委托表示的是一个或多个的方法。


声明委托时确定参数和返回类型，比如 `public delegate int MyDelegate(int x, int y);` 可以用来委托任意一个传入两下整形并返回一个整形的方法。

实例化对象同样需要 `new` 关键字，并传入需要委托的函数名。

静态方法和动态方法都可以被委托。

```c#
namespace SimpleExample
{
    public delegate int MyDelegate(int x, int y);
    class Calc
    {
        public static int Add(int x, int y)
        {
            return x + y;
        }

        public static int Minus(int x, int y)
        {
            return x - y;
        }
    }

    class Program
    {
        static void Main()
        {
            // 创建委托实例
            MyDelegate mdAdd = new MyDelegate(Calc.Add);
            MyDelegate mdMinus = new MyDelegate(Calc.Minus);
            // 使用委托
            Console.WriteLine(mdAdd(1, 2));
            Console.WriteLine(mdMinus(1, 2));
        }
    }
}
```

创建委托实例时，可以不写委托的类型名。比如下面的两种写法是等价的。

```c#
MyDelegate mdAdd = new MyDelegate(Calc.Add);
MyDelegate mdAdd = Calc.Add;
```

委托可以被组合，但其实委托不可以被修改，委托在创建时值就已经确定了。

在通过 `+=` 运算符给委托添加方法后，实际是创建了一个新的委托。

```c#
MyDelegate mdAdd = Calc.Add;
MyDelegate mdMinus = Calc.Minus;
// mdAdd 会被执行，但只有mdMinus会返回值。
MyDelegate mdBoth = mdAdd + mdMinus;
```

如果委托有多个方法，而且有返回值的话，**最后一个方法的返回值**是委托的返回值，其他的返回值都会被忽略。

委托支持引用参数，值**会根据委托列表中的方法而改变**。在调用委托列表的下一个方法时，会将当时的新值传入。

```c#

...
// 注意声明时的ref关键字
public static int Plus(ref int x) => x++;
public delegate int MyDelegate2(ref int x);
...

MyDelegate2 mdPlus = Calc.Plus;
mdPlus += mdPlus;

int x = 1;
mdPlus(ref x);
Console.WriteLine("x: {0}", x); // x: 3
```

### 匿名方法

可以通过delegate来写匿名方法，匿名方法的返回值与委托的类型一致。

```c#
delegate int OtherDel(int InParam);
public void AnonymousMethod()
{
    OtherDel del = delegate (int x) { return x += 20; };
    Console.WriteLine(del(2));
}
```


### Lambda表达式

上面的匿名方法可以写成Lambda表达式。

```c#
OtherDel del = delegate (int x) { return x += 20; };
OtherDel del2 = (int x) => x += 20; // lambda
OtherDel del3 = x => x += 20; // lambda
```