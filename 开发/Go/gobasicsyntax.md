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

* `Logger`接口定义了一个通用的日志记录器接口，它声明了`Log`方法。
* `FileLogger`和`ConsoleLogger`结构体分别实现了`Logger`接口，它们提供了不同的日志记录方式（文件和控制台）。
* 由于`FileLogger`和`ConsoleLogger`都实现了`Logger`接口，我们可以在不修改调用者代码的情况下，灵活地替换日志记录器的实现。这就是多态的概念，它允许我们根据运行时的条件选择合适的实现。
* <mark style="color:blue;">工厂函数是一种设计模式，用于封装对象的创建过程。这样可以使得代码更加灵活和可维护，特别是在涉及到依赖注入或者需要根据不同条件创建不同类型实例的场景。</mark>

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

type Logger interface {
	Log(message string)
}

type FileLogger struct {
	filePath string
}

func (l *FileLogger) Log(message string) {
	log.Println("FileLogger:", message)
}

type ConsoleLogger struct {
	prefix string
}

func (l *ConsoleLogger) Log(message string) {
	log.Println("ConsoleLogger:", message)
}

// 定义一个工厂函数NewLogger，根据配置创建不同类型的日志记录器。
type Config struct {
	LogToFile bool
	FilePath  string
	Prefix    string
}

func NewLogger(config Config) Logger {
	if config.LogToFile {
		return &FileLogger{filePath: config.FilePath}
	} else {
		return &ConsoleLogger{prefix: config.Prefix}
	}
}

func main() {
	config := Config{
		LogToFile: false, // 设置为true以使用文件日志记录器，false以使用控制台日志记录器
		FilePath:  "log.txt",
		Prefix:    "INFO",
	}

	logger := NewLogger(config)

	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		logger.Log("HTTP request received")
		fmt.Fprintf(w, "Hello, World!")
	})

	log.Println("Starting server on :8080")
	log.Fatal(http.ListenAndServe(":8080", nil))
}

```

## 10. 并发神器goroutine和channel

协程（goroutine）是一种轻量级的线程实现，它由 Go 运行时（runtime）管理和调度。协程是 Go 语言并发编程的核心概念，它允许开发者轻松地实现高性能、高并发的程序。

#### 并发（Concurrency）

并发是指多个任务在同一时间段内交替执行。这些任务可能是由同一个进程中的多个线程，或者是由多个进程执行。在单核 CPU 系统中，任务实际上是通过时间片轮转的方式交替执行的，看起来好像是在“同时”进行。在多核 CPU 系统中，任务可以在不同的核心上同时执行，但仍然属于并发范畴，因为这些任务并没有在同一时刻执行。

并发的关键在于任务的交替执行，而不是它们是否在同一时刻执行。例如，在单核 CPU 系统中，两个任务在一个时间片内分别执行一部分，然后交换，这就是并发。

#### 并行（Parallelism）

并行是指多个任务在同一时刻同时执行。这通常需要多个 CPU 核心或多个处理器来完成。在并行计算中，每个任务都在一个独立的核心或处理器上执行，从而实现了任务的真正同步进行。

并行的关键在于任务的同步执行。例如，在一个四核 CPU 系统中，四个任务可以同时在四个不同的核心上执行，这就是并行。

#### 并发与并行的关系

并发和并行之间的关系可以用以下方式描述：

1. 并发是一种更为宽泛的概念，它包括了并行。也就是说，所有的并行都是并发，但并非所有的并发都是并行。
2. 在某些情况下，可以通过增加 CPU 核心数或处理器数量，将并发任务转换为并行任务，从而提高程序的执行效率。
3. 并发编程关注任务的交替执行和资源共享，需要处理竞争条件、死锁等问题。并行编程关注任务的同步执行和数据分解，需要处理数据依赖和通信开销等问题。

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	fmt.Println("In main()")
	go longWait()
	go shortWait()
	fmt.Println("About to sleep in main()")
	time.Sleep(10 * 1e9)
	fmt.Println("At the end of main()")
}
/* goroutine
In main()
About to sleep in main()
Beginning longWait()
Beginning shortWait()
At the end of shortWait()
At the end of longWait()
At the end of main()
*/
/*
In main()
Beginning longWait()
At the end of longWait()
Beginning shortWait()
At the end of shortWait()
About to sleep in main()
At the end of main()

*/

func longWait() {
	fmt.Println("Beginning longWait()")
	time.Sleep(5 * 1e9)
	fmt.Println("At the end of longWait()")
}

func shortWait() {
	fmt.Println("Beginning shortWait()")
	time.Sleep(2 * 1e9)
	fmt.Println("At the end of shortWait()")
}
```

通道（channel）是一种用于在协程之间传递数据的同步原语。goroutine之间通信的桥梁。

无缓冲区：

使用goroutine，自执行函数会跑到一边去执行，当chan需要取的时候，就会往下执行一步。（存一个取一个）

```go
func main() {
	c1 := make(chan int)

	go func() {
		for i := 0; i < 10; i++ {
			c1 <- i
		}
	}()

	for i := 0; i < 10; i++ {
		fmt.Println(<-c1)
	}

}
//0
//1
//2
//3
//4
//5
//6
//7
//8
//9
```

有缓冲区：

在有10个缓冲区的情况下，先存后取，即会先执行自执行的函数，等待缓冲区满了，再进行取。

如果缓冲区不够的情况下，比如只有5个，流程应该是先存5个，然后根据队列的形式，出一个进一个。

```go
func main() {
	c1 := make(chan int, 10)

	go func() {
		for i := 0; i < 10; i++ {
			c1 <- i
		}
	}()

	for i := 0; i < 10; i++ {
		fmt.Println(<-c1)
	}

}
```

前面两个有缓冲区和无缓冲区都是可读可写的，对于仅仅可读和可写的使用方法如下：

```go
var readc <-chan int = c1
var writec chan<- int = c1
```

对于chan是可以关闭的，对于下面的情况，如果提前关闭了，再进行写，便不会生效，如果持续读出的话会出现panic。

```go
func main() {
	c1 := make(chan int, 5)

	c1 <- 1
	c1 <- 2
	c1 <- 3
	close(c1)
	c1 <- 4
	c1 <- 5

	fmt.Println(<-c1)
	fmt.Println(<-c1)
	fmt.Println(<-c1)
	fmt.Println(<-c1)
	fmt.Println(<-c1)

}
```

如果使用for range 读取的话，不适用close会出现死锁

```go
func main() {
	c1 := make(chan int, 5)

	c1 <- 1
	c1 <- 2
	c1 <- 3
	c1 <- 4
	c1 <- 5
	close(c1)

	for c := range c1 {
		fmt.Println(c)
	}

}
```

使用select防止使用chan的时候panic：

如果没有符合条件的，那么就会执行default，如果都符合条件，就会随机执行一个，或者其中几个，或者全部执行。

```go
func main() {
	c1 := make(chan int, 1)
	c2 := make(chan int, 1)
	c3 := make(chan int, 1)
	c1 <- 1
	c2 <- 1
	c3 <- 1
	select {
	case <-c1:
		fmt.Println("c1")
	case <-c2:
		fmt.Println("c2")
	case <-c3:
		fmt.Println("c3")
	default:
		fmt.Println("都不满足")
	}
}
```

goroutine与通道的使用：

```go
func main() {
	c := make(chan int, 1)
	var readC <-chan int = c
	var writeC chan<- int = c
	go SetChan(writeC)
	GetChan(readC)
}

func SetChan(writeC chan<- int) {
	for i := 0; i < 10; i++ {
		writeC <- i
	}
}

func GetChan(readC <-chan int) {
	for i := 0; i < 10; i++ {
		fmt.Printf("In GetChan, get: %d \n", <-readC)
	}
}
```

## 11. 断言Assertion和反射reflect

断言是指把一个接口指定为原始类型。

**断言的基础使用：**

v.(断言为原始类型).调用原始类型方法或者变量

```go
type User struct {
	Name string
	Age  int
	Sex  bool
}

type Student struct {
	User
}

func (u User) SayName(name string) {
	fmt.Println("我的名字是：", name)
}

func main() {
	u := User{
		Name: "LittlePaddy",
		Age:  18,
		Sex:  true,
	}
	check(u)
}

func check(v interface{}) {
	v.(User).SayName(v.(User).Name)
}
```

对断言的使用，常用的方式如下，使用switch case进行使用：

```go
type User struct {
	Name string
	Age  int
	Sex  bool
}

type Student struct {
	Class string
	User
}

func (u User) SayName(name string) {
	fmt.Println("我的名字是：", name)
}

func main() {
	u := User{
		Name: "LittlePaddy",
		Age:  18,
		Sex:  true,
	}
	s := Student{
		"一组",
		User{
			Name: "LittlePaddy",
			Age:  18,
			Sex:  true,
		},
	}
	check(u)
	check(s)
}

func check(v interface{}) {
	switch v.(type) {
	case User:
		fmt.Println("我是User")
		fmt.Println(v.(User).Name)
	case Student:
		fmt.Println("我是Student")
		fmt.Println(v.(Student).Class)
	default:
		fmt.Println("没有符合的")
	}
}
```

**反射（reflection）**是指在**运行时动态地**获取变量的类型信息和值。通过反射，我们可以检查变量的类型，修改其值，以及调用其方法等。Go 的反射功能主要基于 `reflect` 包来实现。

下面是一些常用的取值操作：

```go
type User struct {
	Name string
	Age  int
	Sex  bool
}

type Student struct {
	Class string
	User
}

func (u User) SayName(name string) {
	fmt.Println("我的名字是：", name)
}

func main() {
	u := User{
		Name: "LittlePaddy",
		Age:  18,
		Sex:  true,
	}
	s := Student{"三年二班", u}
	//check(u)
	check(s)
	//fmt.Println(s)
}

func check(inter interface{}) {
	t := reflect.TypeOf(inter)  // 动态获取输入参数接口中的值的类型
	v := reflect.ValueOf(inter) // 获取参数接口中的数据的值
	fmt.Println(t, v)
	for i := 0; i < t.NumField(); i++ {
		fmt.Println(v.Field(i)) // 用来获取值
	}
	fmt.Println(v.FieldByIndex([]int{1, 0})) // 根据层级取值
	tKind := t.Kind()                        // 获取类型
	fmt.Println(tKind)
	if tKind == reflect.Struct {
		fmt.Println("我是Struct")
	}
}
```

下面是通过反射修改值的操作：

```go
func main() {
	u := User{
		Name: "LittlePaddy",
		Age:  18,
		Sex:  true,
	}
	s := Student{"三年二班", u}
	//check(u)
	check(&s) // 如果要修改值的话，需要传递地址
	fmt.Println(s)
}

func check(inter interface{}) {
	v := reflect.ValueOf(inter) // 获取参数接口中的数据的值
	e := v.Elem()
	e.FieldByName("Class").SetString("四年二班")
	fmt.Println(inter)
}
```

下面是通过反射调用方法的使用方式：

```go
func main() {
	u := User{
		Name: "LittlePaddy",
		Age:  18,
		Sex:  true,
	}
	//s := Student{"三年二班", u}
	check(u)
	//check(&s) // 如果要修改值的话，需要传递地址
	//fmt.Println(s)
}

func check(inter interface{}) {
	v := reflect.ValueOf(inter) // 获取参数接口中的数据的值
	m := v.Method(0)
	m.Call([]reflect.Value{reflect.ValueOf("LittlePaddy2")})
}
// 我的名字是： LittlePaddy2
```

## 12. context包的基础使用

在不使用context包的时候，使用通道对子进程进行管理：

```go
func main() {
	flag := make(chan bool)
	message := make(chan int)
	go son(flag, message)
	for i := 0; i < 10; i++ {
		message <- i
	}
	flag <- true
	time.Sleep(time.Second)
	fmt.Println("主进程结束")
}

func son(flag chan bool, msg chan int) {
	t := time.Tick(time.Second) // 用于创建定时器(Ticker)，但是只提供对其滴答通道(ticking channel)的访问
	for _ = range t {
		select {
		case m := <-msg:
			fmt.Printf("接收到值：%d\n", m)
		case <-flag:
			fmt.Println("子进程结束了")
			return
		}
	}
}
```

**WithCancel：**使用`context`来替换`flag`通道。`main`函数中创建了一个带有取消功能的`context`，并将它传递给`son`协程。当`main`函数完成发送数据后，调用`cancel()`函数来通知`son`协程结束。`son`协程通过监听`ctx.Done()`来接收结束信号。

```go
func main() {
	ctx, cancel := context.WithCancel(context.Background())
	message := make(chan int)
	go son(ctx, message)
	for i := 0; i < 10; i++ {
		message <- i
	}
	cancel() // 通知子进程结束
	time.Sleep(time.Second)
	fmt.Println("主进程结束")
}

func son(ctx context.Context, msg chan int) {
	t := time.Tick(time.Second) // 用于创建定时器(Ticker)，但是只提供对其滴答通道(ticking channel)的访问
	for _ = range t {
		select {
		case m := <-msg:
			fmt.Printf("接收到值：%d\n", m)
		case <-ctx.Done():
			fmt.Println("子进程结束了")
			return
		}
	}
}
```

**WithDeadline：**创建一个有截止时间的`context`。当到达截止时间时，`ctx.Done()`会接收到一个信号，表示该`context`已经结束。例如：

```go
deadline := time.Now().Add(5 * time.Second)
ctx, cancel := context.WithDeadline(context.Background(), deadline)
defer cancel()
```

**WithTimeout**：创建一个有超时时间的`context`。当超时到达时，`ctx.Done()`会接收到一个信号，表示该`context`已经结束。例如：

```go
ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()
```

**WithValue**：创建一个可以存储键值对的`context`。这可以用于在协程之间传递元数据。例如：

```go
ctx := context.WithValue(context.Background(), key, value)
```

在协程中，可以使用`ctx.Value(key)`来获取存储的值。但请注意，`context`应该用于传递请求范围的元数据，而不应该用于传递可选参数或配置选项。

## 13. 并发编程sync包的使用

## 14. 文件操作的基础使用

## 15. net包的tcp模块的基础使用

## 16. http创建服务端和客户端

## 17. RPC的客户端和服务端

## 18. 泛型

## 19. 使用go搭建简单的websocket
