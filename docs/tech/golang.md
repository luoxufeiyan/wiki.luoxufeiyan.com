# Golang

## 代码规范

当标识符（包括常量、变量、类型、函数名、结构字段等等）以一个大写字母开头，如：Group1，那么使用这种形式的标识符的对象就可以被外部包的代码所使用（客户端程序需要先导入这个包），这被称为导出（像面向对象语言中的 public）；

标识符如果以小写字母开头，则对包外是不可见的，但是他们在整个包的内部是可见并且可用的（像面向对象语言中的 protected ）。

需要注意的是 `{` 不能单独放在一行，会报错。

### 变量定义

1. Go 中的变量定义，格式为 `var identifier type`。

比如： 

```go
var a int = 1
var b int // int default value: 0
```

2. Go 还可以根据赋值来判断出变量类型，比如： `var c = false`

3. 使用简短变量声明运算符 [Short variable declarations](https://go.dev/ref/spec#Short_variable_declarations) `:= `。


```go
package main

import "fmt"

func main() {
	y := 1
	fmt.Println(y)
}
```
