# 小抄速记
## 列表

### 将类中一个全部成员的值相加

```dart
int total = cartItems.fold(0, (sum, item) => sum + item.amount);
```

```dart
class CartItem {
  final int amount;

  CartItem({this.amount});
}
  CartItem itemOne = CartItem(amount: 10);
  CartItem itemTwo = CartItem(amount: 25);

  List<CartItem> cartItems = [itemOne, itemTwo];


  int total = cartItems.fold(0, (sum, item) => sum + item.amount);
```

Ref: [Clean way to sum a object property value in a list of objects in Dart - Stack Overflow](https://stackoverflow.com/a/59708444/3886059)

### 在列表中查找元素

根据类中的一个成员（比如 id ），找到这个类：

```dart
Book findBook(int id) => list.firstWhere((book) => book.id == id);
```

```dart
void main() {
  final list = List<Book>.generate(10, (id) => Book(id));

  Book findBook(int id) => list.firstWhere((book) => book.id == id);

  print(findBook(2).name);  
  print(findBook(4).name);
  print(findBook(6).name);  
}

class Book{
  final int id;

  String get name => "Book$id";

  Book(this.id);
}
```

ref: [How to find an element in dart list - Stack Overflow](https://stackoverflow.com/questions/59920284/how-to-find-an-element-in-dart-list)


### 更新列表中的元素

在自定义类中更新某一元素，例如通过 uid 更新 food 的数据。

```
foods[foods.indexWhere((element) => element.uid == food.uid)] = food;
```
ref: [dart - How to update a single item in flutter list, as a best way - Stack Overflow](https://stackoverflow.com/a/63180536/3886059)

### 解析JSON的自定类

自定类Category，当JSON返回一个Category的列表时，进行解析。

类定义如下：
```dart
class IceCream {
  int iceCreamId;
  String iceCreamName;

  IceCream({
    this.iceCreamId,
    this.iceCreamName,
  });

  IceCream.fromJson(Map<String, dynamic> json) {
    iceCreamId = json['iceCreamId'];
    iceCreamName = json['iceCreamName'];
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = new Map<String, dynamic>();
    data['iceCreamId'] = this.iceCreamId;
    data['iceCreamName'] = this.iceCreamName;

    return data;
  }
}
```

后端通过JSON返回的`response.data`如下：

```json
[
  {
    "iceCreamId": 147,
    "iceCreamName": "yummy apple"
  },
  {
    "iceCreamId": 148,
    "iceCreamName": "good ice"
  },
  {
    "iceCreamId": 149,
    "iceCreamName": "Hanna ice"
  }
]
```

可以通过如下方式保存在`List<IceCream>`中：
```dart
List<IceCream> _iceCreamList = List<IceCream>.from(
      response.data.map((e) => IceCream.fromJson(e)));
```

ref: [dart - How to Deserialize a list of objects from json in flutter - Stack Overflow](https://stackoverflow.com/a/58720667/3886059)

一个 json 转 dart 的工具[JSON to Dart](https://javiercbk.github.io/json_to_dart/)