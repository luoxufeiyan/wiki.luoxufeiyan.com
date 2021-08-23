
# 布局

### 异形屏边界问题

使用[SafeArea](https://api.flutter.dev/flutter/widgets/SafeArea-class.html) 适配异形屏，设置`SafeArea`的四个方向是否设立安全区。

例如：

```dart
  @override
  Widget build(BuildContext context) {
    return SafeArea(
      bottom: false,
      top: true,
    );
  }
```

ref:[Flutter SafeArea - 异形屏适配利器](https://juejin.im/post/6844903849996582926)

### 根据手机屏幕动态调整大小

更灵活的编码布局：

导入：

```dart
import 'package:flutter_screenutil/flutter_screenutil.dart';
```

在build中添加一行：


根据屏幕尺寸适配字体大小：`screenutil().setsp`，同样可以适配高度和宽度。

```
适配后的宽度width: ScreenUtil().setWidth(540),
适配后的高度height: ScreenUtil().setHeight(200),
```

同样方法可以创建灵活的，可变大小的点位符：

```dart
VEmptyView(ScreenUtil().setHeight(30))
```

同样字体和窗口大小也可用这种方法适配。


在build中动态初始化页面大小：

```dart
  @override
  Widget build(BuildContext context) {
    ScreenUtil.init(context, width: 1080, height: 1920, allowFontScaling: true);
    return SafeArea( ...
```

[flutter 屏幕尺寸适配 字体大小适配](https://juejin.im/post/6844903693955891208)

### 灵活的弹性布局

`Expanded()`，可以根据弹性系数`flex`来动态分配空间。

#### Flexible

可以解决文本区`overflow`（`overflow: TextOverflow.ellipsis,`）不生效的问题。将文本所在的Column外包裹一个`Flexible`。

### Col 和 Row 布局

[Flutter中MainAxisAlignment和CrossAxisAlignment详解_喻志强的博客-CSDN博客](https://blog.csdn.net/yuzhiqiang_1993/article/details/86496145)