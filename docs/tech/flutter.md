# Flutter

## 变量&语法

### 函数定义

```dart
返回类型  方法体  (参数1,  参数2, {可选命名参数1,  可选命名参数2,}){
    方法体...
    return 返回值
}

String newPerson(String name, int age, {bool gender=0, String location}){
  // func code here
  return name;
}
```





### GlobalKey

GlobalKey能够跨Widget访问状态。可以在外部定义一个GlobalKey，然后在需要绑定的Widget中使用：

```dart
SwitcherWidget(
        key: key,
      ),
```

绑定这个widget，并可以在外部调用这个widget的方法，来改变这个Widget的状态。





例如一个用户输入表格，需要在用户输入后验证合法性，也需要在用户点击确认按钮后向API提交请求，即需要用GlobalKey。



ref:

[Flutter--&gt; 何时使用GlobalKey？ - 简书](https://www.jianshu.com/p/d37f97a926a8)

### State

#### Stateful Widget

创建一个Stateful Widget需要两个类，分别继承自StateFulWidget和State。

[Flutter学习笔记（三）-- 事件交互和State管理 - 简书](https://www.jianshu.com/p/ed9c3378e9cc)

#### initState()

在Stateful Widget的第二个类（继承自StateFulWidget中的那个）中，`initState()`会在页面渲染时执行，因此对于一些不改变的常量，可以放在`initState()`中，避免每次Widget tree更新后都会对常量赋值。

在initstate()中使用provider时，需要将函数包裹在`WidgetsBinding.instance.addPostFrameCallback((timeStamp)`中，避免在异步函数调用时将UI冻结。eg:
```dart
  @override
  void initState() {
    selectedStore = Provider.of<CurrentStoresProvider>(context, listen: false)
        .getSelectedStore;
    WidgetsBinding.instance.addPostFrameCallback((timeStamp) async {
      await Provider.of<CurrentMenuProvider>(context, listen: false)
          .getMenuFromAPI(context, selectedStore.storeId); // this line will freeze the UI withour wrapped by the WidgetsBinding
    });

    super.initState();
  }
```

除了`StatefulWidget`的`setState()`外，还可以通过`StatefulBuilder(builder: (ctx, setItemState) { return Container()}`来定义Container()中的state，当内容改变时重新渲染Container()部分。

而且，通过`StatefulBuilder`定义的`setItemState`还可以被子类继承。一个页面中可以存在多个state，且state之间可以有包含关系。



#### didChangeDependencies()

会在变量改变后刷新，如果用provider的话，需要设置listen为true生效。



#### 异步

注意在`setState()`中，不能进行`async`异步。TODO

#### 路由管理

[2.2：路由管理 · 《Flutter实战》](https://book.flutterchina.club/chapter2/flutter_router.html)





## Ref


### Plugins

[Awesome Flutter Snippets](https://marketplace.visualstudio.com/items?itemName=Nash.awesome-flutter-snippets)

### Doc

flutter tutorials:

  * https://flutter.dev/docs/get-started/install
  * https://flutter.dev/docs/development/ui/layout/tutorial
  * https://flutter.dev/docs/development/ui/interactive
  * https://flutter.dev/docs/development/ui/assets-and-images
  * https://flutter.dev/docs/development/ui/navigation
  * https://flutter.dev/docs/development/data-and-backend/state-mgmt/intro
  * https://flutter.dev/docs/development/data-and-backend/json


中文资料：

* [简介 · 《Flutter实战》](https://book.flutterchina.club/) 