# 空安全

## 声明变量

与之前一致，但默认不能为空

```dart
int i = 1024;
String s = 'Hi';
final b = func();
```

声明可为空的变量，需要在变量类型前加？

```dart
int? i = 1024; // can be null later
String? s ;
final? b = func(); // func may return null
```

尽量不要将变量设置为可空（减少？的使用），绝大多数类型都是可以不必为空的。



## 对空赋值



使用`？？`对变量赋值，如果变 量为空，则赋右侧值，否则为运算符左值。

```dart
int value = aNullableInt ?? 0; // 0 if it's null; otherwise, the integer
```

同样还有`？？=`

```dart
int value ??= 0; // 0 if it is null, oterwise, keep the original value
```

