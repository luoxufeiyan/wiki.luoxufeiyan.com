# 协变

C# 中对于对象（即对象引用），仅存在一种隐式类型转换，即 **子**类型的对象引用到**父**类型的对象引用的转换。所以协变指的是**从子到父**的类型转换。

### 赋值兼容性

可以将派生类的对象的实例赋值给基类的变量，这称为赋值兼容性。比如可以把派生类的 Dog 赋值成基类的 Animal（实际类型依然是 Dog）。

```c#
public class Covariance
{
   class Animal
   {
      public int NumOfLegs = 4;
   }

   class Dog : Animal
   {

   }

   public void Run()
   {
      Animal a = new Animal();
      Animal b = new Dog();

      Console.WriteLine("Legs: {0}", b.NumOfLegs);
   }
}
```

## 协变

尽管有赋值兼容性，但是如果将派生类型构造的委托赋值给基类构造的委托，编译器则会报错。

```c#
class Animal
{
   public int NumOfLegs = 4;
}

class Dog : Animal
{

}

delegate T Factory<T>();

static Dog MakeDog() => new Dog();

public void Run2()
{
   Factory<Dog> dogMaker = MakeDog;
   Factory<Animal> animalMaker = dogMaker;
   Console.WriteLine("Legs: {0}", animalMaker().NumOfLegs.ToString());
}
```

`Factory<Animal> animalMaker = dogMaker;` 报错：

> 无法将类型“Playground.Covariance.Factory<Playground.Covariance.Dog>”隐式转换为“Playground.Covariance.Factory<Playground.Covariance.Animal>” [Playground]

这是因为，尽管 Dog 是 Animal 派生类，但是委托`Factory<Dog>`不是从`Factory<Animal>`派生的。这两个委托是同级的，从 delegate 类派生出的。

所以，如果派生类做为输出值，而调用代码期望得到他的基类引用，这种委托有效性的关系就是协变。

需要在委托的声明中加上 `out` 关键字，这样编译器就会把这个委托转换为协变的：`delegate T Factory<out T>();`。

### 数组协变

满足下面的条件时，可以将**不是**数组基类型的元素赋值给数组，称之为数组协变 array covariance。

- 当数组是引用类型数组。
- 被赋值的类型和数组的基类型之间有隐式或显式转换。

```c#
 class A { ... } // Base class
 class B : A { ... } // Derived class

 class Program {
 static void Main() {
    // Two arrays of type A[]
    A[] AArray1 = new A[3];
    A[] AArray2 = new A[3];

    // Normal--assigning objects of type A to an array of type A
    AArray1[0] = new A(); AArray1[1] = new A(); AArray1[2] = new A();

    // Covariant--assigning objects of type B to an array of type A
    AArray2[0] = new B(); AArray2[1] = new B(); AArray2[2] = new B();
    }
 }
```

## Ref:

- https://segmentfault.com/a/1190000007005115
