# 交互

### 加载动画 FadeInImage

通过`FadeInImage`在部件（比如图片）加载时展示一个动画。

[Fade in images with a placeholder  - Flutter](https://flutter.dev/docs/cookbook/images/fading-in-images)

### 控制组件可见性

可以用`Visibility()`实现，其中的`visible:_isVisible`变量控制元件的可见性，注意改变变量`_isVisible`值时需要用`setState()`。

[Flutter - Hide / Show Widget Using Visibility](https://www.woolha.com/tutorials/flutter-hide-show-widget-using-visibility)




### 按钮事件

#### Flatbutton

设置按钮事件时为`onPressed: () {_setAdminVisibilityStatus();},`，其中将`State`函数写在大括号内，异步操作写为`onPressed: () async {_setAdminVisibilityStatus();},`。

#### InkWell

`InkWell`同样可以做按钮使用，可以更好地控制按钮文本的位置，处理文本对齐的情况。


[How to align text in a button in flutter? - Stack Overflow](https://stackoverflow.com/questions/56267502/how-to-align-text-in-a-button-in-flutter)

[3.4：按钮 · 《Flutter实战》](https://book.flutterchina.club/chapter3/buttons.html)

### 获取用户输入

通过`TextEditingController`控制用户输入：[处理文本输入- Flutter中文网](https://flutterchina.club/text-input/)

### ScrollController


在为`scrollcontroller`设置`addListener()`监听事件时，如果使用的是`ListView.builder`(或者GridView)，需要在`ListView.builder`外设置一个Container并设置高度！否则监听事件不生效。

ref: [Flutter listview builder Scroll controller listener not firing inside list view? - Stack Overflow](https://stackoverflow.com/a/62595072/3886059)                      

## 异步加载

FutureBuilder可以通过异步函数来渲染UI，在future中传入一个异步操作，然后在builder中，可以通过`asyncData.connectionState`或者`async.hasData`来分别判断异步函数是否结束，或者异步函数是否返回了数据。分别根据这两种情况return不同的widget

```dart
body: FutureBuilder(
              future: _getMenuFromAPIFuture, // 避免多次被 call ，实例化一个 future 类型。
              builder: (ctx, asyncData) {
                if (asyncData.connectionState != ConnectionState.done)
                  return Center(child: CircularProgressIndicator()); // 执行异步时加载一个进度条

                return _homeScreenContent(); // 显示结果
              })),
```

`_getMenuFromAPIFuture`是一个在`initState`中被定义的 Future 类型。


与FutureBuilder类似，StreamBuilder也依赖异步事件进行UI的更新，他可以监听多个异步事件的结果，也可以展示异步事件的不同进度，可以用来实现动态刷新的效果，或者用来显示一个异步事件（比如网络下载）的进度条。

Ref https://book.flutterchina.club/chapter7/futurebuilder_and_streambuilder.html