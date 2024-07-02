# 🪨 GoBasicSyntax

## 1. 基础知识——结构、包、变量

### 1.1 结构

官方推荐的项目结构：

```
pkg # 存放包的目录
src # 存放项目的目录
bin # 存放可执行文件的目录
```

### 1.2 变量的定义

对于一个string类型变量的声明如下：

```go
var a string = "hello world"
```

&#x20;<mark style="color:blue;">声明格式</mark>：\[关键字 变量名 变量类型 = 变量值]<mark style="color:red;">（显示变量的声明）</mark>

```go
b := "hello world"
```

<mark style="color:blue;">声明格式</mark>：\[变量名 := 变量值]<mark style="color:red;">（隐式变量声明）</mark>

### 1.3 关键字

关键字不能用作变量名，比如var。

### 1.4 包

> 在Go里面，对于包中变量名和函数（方法）名的定义，如果是大写的，说明是公有的，可以被别的包调用，如果是小写的，则不能被调用。

下面是一个调用包中变量的示例：

```go
// 目录
- testpackage
- -testpackage.go
- main.go
```

```go
// testpackage.go
package testpackage

var A string = "测试"
```

```go
// main.go
package main

import (
    "fmt"
    "goclass/testpackage"
    // 这里对包的调用有三种，上面为第一种（最常用）
    // 第二种（别名）：testA "goclass/testpackage"
    //                    fmt.Println(testA.A)
    // 第三种（全部引入）：. "goclass/testpackage"
    //                   fmt.Println(A)
)

func main(){
    fmt.Println(testpackage.A)
}
```

## 2. 基本数据类型和变量

## 3. 流程控制

## 4. 数组和切片

## 5. map的声明和使用

## 6. 函数func方法

## 7. 指针和地址

## 8. 结构体struct声明和使用

## 9. 接口interface

## 10. 并发神器goroutine和channel

## 11. 断言Assertion和反射reflect

## 12. context包的基础使用

## 13. 并发编程sync包的使用

## 14. 文件操作的基础使用

## 15. net包的tcp模块的基础使用

## 16. http创建服务端和客户端

## 17. RPC的客户端和服务端

## 18. 泛型

## 19. 使用go搭建简单的websocket
