# 基础

## 视图函数

- 通过装饰器（推荐）

通过装饰器 `@app.route()`，为 view 函数定义路由，在装饰器中传入URL。

视图函数类比于MVC的controller。

eg：
```
@app.route('/index')
def index():
    return "Here is the index page."
```

- `add_url_rule`添加规则

```
def index():
    return "Here is the index page."
app.add_url_rule('/index', view_func=index)
```

对于即插视图使用这种方法。

### 基于类的视图（即插视图）

OOP的类方便继承，而函数不方便继承。主流写法是写一个基类，然后在子类中复用代码。

### 解决用户访问请求兼容问题

如上eg，用户访问 `/index` 正常，访问`/index/`则会404。

解决方法为改写成` @app.route('/index/')`，flask会对`/index`301重定向到`/index/`，即`唯一URL原则`。

### 唯一URL原则

一个视图函数（页面，资源）只可对应一个URL，若对应多个URL（例如`/index`请求不经过301直接转到`/index/`），则不利于SEO。

## 自动重启（热启动）

`app.run(debug=True)`，开启debug模式，文件改动后自动重启。

## flask配置文件

`app.config.from_object()`载入配置文件，读取配置文件时用`app.config['HOST/PORT/OTHER_CONF']`方法。

## 主执行文件判断

只在入口文件中执行，使不同环境下用不同httpd(沙盒、生产)，避免在apache+uwsgi下执行文件使flask server启动。

```
if __name__ == '__main__':
    app.run(host='0.0.0.0', debug=True)
```