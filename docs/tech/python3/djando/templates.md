# templates 模板

  * Django会遍历所有app的templates文件夹来查找文件，因此容易发生冲突。

解决方法：在templates文件夹中建立app文件夹。

  * 通过`Django 上下文渲染器`将变量共享给多个页面使用。

## 格式
```
{{ 变量 }}

{% 模板标签 %} 例如条件判断。
```
