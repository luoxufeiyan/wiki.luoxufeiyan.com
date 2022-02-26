# 协变

C# 中对于对象（即对象引用），仅存在一种隐式类型转换，即 **子**类型的对象引用到**父**类型的对象引用的转换。所以协变指的是**从子到父**的类型转换。

## 数组协变

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
