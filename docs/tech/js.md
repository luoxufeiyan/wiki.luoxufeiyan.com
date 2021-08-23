# JavaScript

## 数据结构

### 数字

数字为`双精度 64 位格式`，不存在整形。

一个看上去是整数的东西，其实都是浮点数。



### 运算符

#### 相加

+号可以用来拼接字符串，例如：

`"hello" + "world"; //"helloworld"`

但如果用`字符串`加上`数字`（或其他值），那么操作数都会被首先转换为字符串。

例如：

`"1" + 1 + 2; //"112"`

如果是数字相加则会返回数字：

`1 + 2 + "1";//"31"`

#### 相等

两等号时会转换数据类型：

`123 == "123" // true`



三等号时不会自动类型转换：

`123 === "123"; // false`



### 声明变量

用`let`，`const`和`var`声明一个新变量。

const声明常量，`let`声明的变量只在`块内`（for loop）生效，`var`声明的变量在块外也有效，是最常见的声明方法。

let声明：

```
// myLetVariable is *not* visible out here

for (let myLetVariable = 0; myLetVariable < 5; myLetVariable++) {
  // myLetVariable is only visible in here
}

// myLetVariable is *not* visible out here

```

var声明：

```
// myVarVariable *is* visible out here

for (var myVarVariable = 0; myVarVariable < 5; myVarVariable++) { 
  // myVarVariable is visible to the whole function 
} 

// myVarVariable *is* visible out here 
```




# Ref:

* [A re-introduction to JavaScript (JS tutorial) - JavaScript | MDN](