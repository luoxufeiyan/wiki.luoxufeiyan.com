# BootStrap4

## navbar

右对齐特定一个元素可在`<nav>`中定义两个`<ul>`（一个为左侧正常菜单，一个为右对齐菜单），并将左侧菜单设置class为`mr-auto`。

```
<nav class="navbar navbar-expand-sm bg-dark navbar-dark fixed-top">

        <!-- Links -->
        <ul class="navbar-nav mr-auto">
            <li class="nav-item">
                <a class="nav-link navbar-brand" href="#">Home</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Create</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Search</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Help</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">About</a>
            </li>
        </ul>
        <!-- The right items -->
        <ul class="navbar-nav">
            <li class="nav-item">
                <a class="nav-link" href="#">Login</a>
            </li>
        </ul>

    </nav>
```

Ref: [css - Bootstrap 4 align navbar items to the right - Stack Overflow](https://stackoverflow.com/questions/41513463/bootstrap-4-align-navbar-items-to-the-right)

