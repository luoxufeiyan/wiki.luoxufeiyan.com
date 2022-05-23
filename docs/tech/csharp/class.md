# 类 Class

类是引用类型，意味着数据引用和实际数据都在申请内存。

字段是类里面的变量。

与C和cpp不同，c#在类型的外部不能声明全局变量（也就是变量或字段）。所有的**字段都属于类型**，而且必须在类型声明内部声明。

同样的，c#中 **没有全局函数（也就是方法或函数)** 声明在类型声明的外部。

## 访问修饰符：

指定成员的访问级别。

* private (默认)，只有类内部可访问。
* public 可以被其他对象访问。
* protected 只有类内部和类派生出的子类可以访问。
* internal 只有程序集（assembly）内的类可以访问。
* protected internal == protected + internal 派生出的子类和程序集内的类可以访问。

ref: [Access Modifiers - C# Programming Guide | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers)

抽象成员

## 继承

已存在的类称为基类（base class），新的类称为派生类（derived class）。

派生类包括基类的成员和派生类中声明的成员。所有的类都派生自 object 类。

### 访问继承的成员

在派生类中，基类的成员可以被访问到，就像是派生类自己的成员一样。

例，派生类的四个成员都可以被访问，不管是在基类中声明还是在派生类中声明。

```c#
namespace SimpleExample
{
    class MyBaseClass
    {
        public string BaseclassText = "base class text;";
        public void BaseClassMethod(string value)
        {
            Console.WriteLine("Base class write: "+ value);
        }
    }

    class MyDerivedClass : MyBaseClass
    {
        public string DerivedclassText = "derived class text;";
        public void DerivedClassMethod(string value)
        {
            Console.WriteLine("Derived class write: " + value);
        }
    }
    
    class Program
    {
        static void Main()
        {
            MyDerivedClass md = new MyDerivedClass();
            md.BaseClassMethod(md.BaseclassText);
            md.BaseClassMethod(md.DerivedclassText);
            md.DerivedClassMethod(md.BaseclassText);
            md.DerivedClassMethod(md.DerivedclassText);
        }
    }
}
```

输出：
```cmd
Base class write: base class text;
Base class write: derived class text;
Derived class write: base class text;
Derived class write: derived class text;
```

### 屏蔽基类的成员

可以通过在派生类中新建一个同名的成员来屏蔽基类成员。需要使用 `new` 修饰符告诉编译器需要屏蔽基类成员。


屏蔽数据成员，需要声明一个同类型的成员并使用相同的名称。

例如：
```c#
namespace SimpleExample
{
    class MyBaseClass
    {
        public string ClassText = "From base class.";
    }

    class MyDerivedClass : MyBaseClass
    {
        new public string ClassText = "Hide from derived class.";
    }
    
    class Program
    {
        static void Main()
        {
            MyDerivedClass md = new MyDerivedClass();
            Console.WriteLine(md.ClassText);
        }
    }
}
```

屏蔽函数成员，在派生类中声明一个相同签名的函数成员。

```c#
namespace SimpleExample
{
    class MyBaseClass
    {
        public string classText = "base class text;";
        public void ClassMethod(string value)
        {
            Console.WriteLine("Base class write: "+ value);
        }
    }

    class MyDerivedClass : MyBaseClass
    {
        new public string classText = "hide from derived class text;";
        new public void ClassMethod(string value)
        {
            Console.WriteLine("Derived class write: " + value);
        }
    }
    
    class Program
    {
        static void Main()
        {
            MyDerivedClass md = new MyDerivedClass();
            md.ClassMethod(md.classText); //屏蔽基类访问
        }
    }
}
```

输出：

```cmd
Derived class write: hide from derived class text;
```

### 基类访问 base access

继续访问被隐藏的基类成员，可以在使用基类访问表达式，使用 base 关键字加成员名。

尽量避免使用这个特性。

例如：
```c#
namespace SimpleExample
{
    class MyBaseClass
    {
        public string ClssText = "base class text;";
    }

    class MyDerivedClass : MyBaseClass
    {
        new public string ClssText = "hide from derived class text;"; //屏蔽基类成员
        public void PrintMethod()
        {
            Console.WriteLine(ClssText);
            Console.WriteLine(base.ClssText); // 基类访问
        }
    }
    
    class Program
    {
        static void Main()
        {
            MyDerivedClass md = new MyDerivedClass();
            md.PrintMethod();
        }
    }
}
```

输出：

```cmd
hide from derived class text;
base class text;
```

### 虚方法和覆写

当使用基类引用访问派生类对象时，得到的是基类的成员。虚方法可以使基类的引用访问“升至”派生类内。

在基类方法前加上 `virtual` 关键字，表示虚方法。在派生类中加 `override` 表示覆写这个虚方法。

例如：

```c#
namespace SimpleExample
{
    class MyBaseClass
    {
        virtual public void Print()
        {
            Console.WriteLine("Base class write.");
        }
    }

    class MyDerivedClass : MyBaseClass
    {
        override public void Print()
        {
            Console.WriteLine("Derived class write.");
        }
    }
    
    class Program
    {
        static void Main()
        {
            MyDerivedClass md = new MyDerivedClass();
            MyBaseClass bc = (MyBaseClass)md;
            MyBaseClass bc2 = new MyBaseClass();
            md.Print();
            bc.Print();
            bc2.Print();
        }
    }
}
```

基类的方法被覆写，对基类的调用实际上调用了子类中的方法，输出：

```cmd
Derived class write.
Derived class write.
Base class write.
```


## 结构

结构与类相似，也包括数据成员和函数成员，与类最主要的区别是：

* 结构不能被继承，（因为结构是隐式密封的）。
* 类是引用类型，而结构是值类型：成例化后被存放在**栈**中。

将一个结构体赋值给另一个结构体是，是在栈中开一块内存并将结构体的值完全复制到这块内存中，不是指针引用，类似 deep copy 。

