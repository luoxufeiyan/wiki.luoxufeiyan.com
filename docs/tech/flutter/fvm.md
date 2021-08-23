# fvm

fvm是一个 flutter 版本管理工具，类似于 python 的anaconda。可以方便的切换 flutter 版本。





## 安装

Ref: [leoafarias/fvm: Flutter Version Management: A simple CLI &amp; GUI to manage Flutter SDK versions.](https://github.com/leoafarias/fvm#usage)

然后添加环境变量。

```bash
 # Use flutter fvm
 export PATH="$PATH":"$HOME/fvm/default/bin"
 export PATH="$PATH":"$HOME/.pub-cache/bin"
```

第一行为默认版本的 flutter，只在 fvm 设置默认 flutter 版本后生效。

第二行为 fvm 的环境变量。



## 使用

### 安装版本

* 列出所有的 flutter 版本： `fvm releases`

* 安装指定版本的flutter：`fvm install <version>`

* 列出本机安装的所有版本： `fvm list`



### 使用环境内 flutter

* 对某一个项目使用指定版本：在项目根目录下使用`fvm use <version>`

* 设置本机的全局版本（default 版本）：`fvm use <version> --global`



在项目目录中使用 flutter ，需要使用`fvm flutter` 代替`flutter`命令。



例如：



需要执行`flutter build web`，则在 fvm 中为`fvm flutter build web`