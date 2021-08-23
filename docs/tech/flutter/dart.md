# Dart语法

## 运算符重载

dart 知道 1 + 2 = ? 中的 + 如何处理，但对于 class StudentGrade ，可以通过运算符重载的方式定义 StudentGrade + StudentGrade = ? 中的加号逻辑。

定义类的两个对象如何做运算。 

例如通过 id 判断两元素相等。

```dart
class FruitItem {
  int fruitItemId;
  String fruitItemName;
 
  FruitItem({
    this.fruitItemId,
    this.fruitItemName,
  });
 
  bool operator ==(o) => o is FruitItem && o.fruitItemId == fruitItemId;

}
```

等同于： 
```dart
  bool operator ==(FruitItem o) {
    return this.fruitItemId == o.fruitItemId;
  }
```

ref: 

* [https://medium.com/@dumazy/enhance-your-classes-with-operator-overloading-in-dart-f1124bd813a0](https://medium.com/@dumazy/enhance-your-classes-with-operator-overloading-in-dart-f1124bd813a0)

* [https://www.jianshu.com/p/d7b7e490a5ad](https://www.jianshu.com/p/d7b7e490a5ad)
