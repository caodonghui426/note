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

基本数据类型：整数类型、浮点类型、字符串类型、布尔类型

## 3. 流程控制

## 4. 数组和切片

### 4.1 数组

数组的定义：

```go
a := [3]int{0, 1, 2}
// [元素长度]元素类型{元素1，...}
b := [...]int{1, 2, 3, 4, 5}
// 如果不确定数组的长度，可以用...代替
var c = new([3]int) // 返回的是一个指针
d[2] = 3
// &[0, 0, 3]
```

数组的遍历：

```go
for i := 0; i < len(b); i++{
    fmt.Println(b[i])
}

for i, v := range b{
    fmt.Println(i) // 数组下标
    fmt.Println(v) // 数组值
}
```

二维数组和多维数组：

```go
er := [3][3]int{
    {0, 1, 2},
    {4, 5, 6},
    {7, 8, 9},
}
```

### 4.1 切片

切片是不固定的数组

```go
a := [3]int{0, 1, 2} // 数组
cl := a[0:2] // 左开右闭
cl = append(cl, 4) // 只有切片可以使用append
```

拷贝copy：

```go
a := [5]int{0, 1, 2, 3, 4}
a1 := a[0:3] // [0, 1, 2]
a2 := a[2:4] // [2, 3]
copy(a1, a2) // [2, 3, 2] 覆盖对应位置
```

切片的定义方式：

```go
// 1. 直接定义：没有默认值
var a = []int 
append(a, 0)
// 2. make定义：有默认值 0
a := make([]int, 4)
```

## 5. map的声明和使用

```go
// 声明方式1:
var m map[string]string
m = map[string]string{} // 使用第一种方式需要对 m 进行初始化操作，否则会导致运行时出错

m := map[string]string{}

m := make(map[string]string)

// map[key]value{}
```

map 中元素的删除：

```go
delete(m, "head")
// delete(变量名， key)
```

map 中元素的循环：

```go
for k, v := range m {
    fmt.Println(k, v)
}
```

## 6. 函数func方法

在函数 func 中，如果在定义了返回值，那么只需 return 即可：

```go
func a(data1 int, data2 int)(ret1 int, ret2 int) {
    ret1 = data1
    ret2 = data2
    return
}
```

匿名函数：

```go
func main(){
    a := func(data string) {
        fmt.Println(data)
    }
}
```

不定向参数，也称为可变参数或参数个数可变的参数，它允许函数或方法接收不确定数量的参数。

```go
func a(data1 int, data2 ...sring) {
    for k, v range data2{
        fmt.Println(k, v)
    }
}
```

自执行函数：

```go
func main(){
    (func(){
        fmt.Println("这里是自执行函数")
    })()
}
```

闭包函数：

```go
func a()func(int){
    return func(int){
        fmt.Println("闭包函数", num)
    }
}
func main(){
    a()(1) // 闭包函数 1
}
```

延迟函数：

```go
func a() {
    fmt.Println("我是被延迟调用的")
}
```

## 7. 指针和地址

**地址**：\
地址是内存中存储数据的位置标识。每一个变量在内存中都有一个特定的地址，通过这个地址可以找到并操作存储在该位置的数据。\
**指针**：\
指针是一种变量，它存储的是另一个变量的地址。

```go
var num int = 10
var ptr *int = &num
*ptr = 20  // 修改 num 的值
```

**数组指针和指针数组**：

```go
var arr [5]int
arr = [5]int{1, 2, 3, 4, 5}

var arrPtr *[5]int // 数组指针
arrPtr = &arr // &[1, 2, 3, 4, 5]

var ptrArr [5]*int // 指针数组
a := 1
b := 2
c := 3
d := 4
e := 5
ptrArr = [5]*int{&a, &b, &c, &d, &e}
fmt.Println(ptrArr) //[0xc00009e018 0xc00009e020 0xc00009e028 0xc00009e030 0xc00009e038]
*ptrArr[4] = 0
fmt.Println(e) // 0
```

## 8. 结构体struct声明和使用

结构体的定义方式：

```go
type A struct {
    Name string
    Age int
    Sex bool
} 
func main(){
    // 定义方式1
    var a A
    a.Name = "LittlePaddy"
    a.Age = 23
    a.Sex = true
    fmt.Println(a)
    // 定义方式2
    a1 := A{
        "LittlePaddy",
        23,
        true,
    }
    // 定义方式3
    a2 := A{
        Name: "LittlePaddy",
        Age: 23,
        Sex: true,
    }
    // 定义方式4
    a3 := new(A)
    a3.Name = "LittlePaddy"
    fmt.Println(a3) // &{LittlePaddy 0 false}返回地址
}
```

结构体与指针：

<pre class="language-go"><code class="lang-go"><strong>type A struct {
</strong>    Name string
    Age int
    Sex bool
} 
func main(){
<strong>    a := A{
</strong>        Name: "LittlePaddy",
        Age: 23,
        Sex: true,
    }
    var aPtr *A
    aPtr = &#x26;a
    a.Name = "LittlePaddy is handsome"
    fmt.Println(a) // {LittlePaddy is handsome 23 true}
    aPtr.Name = "LittlePaddy is very handsome"
    fmt.Println(a, aPtr) // {LittlePaddy is very handsome 23 true} &#x26;{LittlePaddy is very handsome 23 true}
    (*aPtr).Name = "LittlePaddy is very very handsome"
    fmt.Println(a, *aPtr) //{LittlePaddy is very very handsome 23 true} {LittlePaddy is very very handsome 23 true}
}
</code></pre>

结构体方法：

<pre class="language-go"><code class="lang-go">type A struct {
    Name string
    Age int
<strong>    Sex bool
</strong>} 
func (a *A)Song(name string)(restr string){
    restr = "非常好"
    fmt.Printf("%v 唱了一首 %v，观众觉得 %v", a.Name, name, restr)
    return restr
}
func main(){
    a := A{
        Name: "LittlePaddy",
        Age: 23,
        Sex: true,
    }
    fmt.Println(a.Song("若是月亮还没来"))
}
</code></pre>

## 9. 接口interface

在Go语言中，接口是一种抽象类型，它定义了一组方法的签名，但不包含这些方法的实现。主要特点和作用包括：

* 定义行为规范
* 实现多态性
* 解耦代码

```go
package main

import "fmt"

// 定义接口
type Shape interface {
    Area() float64
}

// 圆形类型
type Circle struct {
    Radius float64
}

// 实现接口的 Area 方法
func (c Circle) Area() float64 {
    return 3.14 * c.Radius * c.Radius
}

// 矩形类型
type Rectangle struct {
    Width  float64
    Height float64
}

// 实现接口的 Area 方法
func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

func printArea(s Shape) {
    fmt.Println("面积:", s.Area())
}

func main() {
    c := Circle{Radius: 5}
    r := Rectangle{Width: 4, Height: 6}

    printArea(c)
    printArea(r)
}
```

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
