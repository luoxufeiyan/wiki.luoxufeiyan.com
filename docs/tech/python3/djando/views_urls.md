# 视图与网址

## 项目 project 与应用 app 区别

项目与应用的区别：一个项目中可以包含多个应用，应用是指功能性的划分模块。如一个电商网站可以作为一个项目，其中的日志系统，购物车系统都可以分割成独立的应用。

## 应用添加

注意需要把 app 添加到 project 的` settings.INSTALLED_APPS`中。

新添加的 app 需要加入项目的 settings.py 中的 INSTALL_APPS 中：

```
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'learn',
)
```

使项目能够找到应用的模板文件。

## URL 规范

Werkzeug 路由模块，URL 以虚线结尾。

Flask 例：

```
@app.route('/projects/')
def projects():
    return 'The project page'

@app.route('/about')
def about():
    return 'The about page'
```

虽然它们看起来确实相似，但它们结尾斜线的使用在 URL 定义 中不同。第一种情况中，规范的 URL 指向 projects 尾端有一个斜线。这种感觉很像在文件系统中的文件夹。访问一个结尾不带斜线的 URL 会被 Flask 重定向到带斜线的规范 URL 去。

然而，第二种情况的 URL 结尾不带斜线，类似 UNIX-like 系统下的文件的路径名。访问结尾带斜线的 URL 会产生一个 404 “Not Found” 错误。

当用户访问页面时忘记结尾斜线时，这个行为允许关联的 URL 继续工作，并且与 Apache 和其它的服务器的行为一致。另外，URL 会保持唯一，有助于避免搜索引擎索引同一个页面两次。

[外部链接](https://www.kancloud.cn/hartnett/flask/131483)
