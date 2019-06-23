+++
title = "Golang 速食指南"
date = 2019-06-22T04:42:41.850Z
author = "horochx" 
cover = ""
tags = ["golang", "速食指南"]
description = "Go 是 Google 于 2009 年 11 月 10 日发布的一门静态强类型、编译型、并发型，并具有垃圾回收功能的编程语言，现在被广泛应用在服务端领域。通过 <a href=\"https://trends.google.com/trends/explore?date=today%205-y&q=%2Fm%2F09gbxjr\" target=\"_blank\">Google Trends</a> 可以看出来，在过去 5 年，Go 的热度始终在上升。通过以下内容，我们可以快速了解一下 Go 语言的基础特性，然后来决定是否深入地学习它。"
showFullContent = false
+++

Go 是 Google 于 2009 年 11 月 10 日发布的一门静态强类型、编译型、并发型，并具有垃圾回收功能的编程语言，现在被广泛应用在服务端领域。通过 <a href="https://trends.google.com/trends/explore?date=today%205-y&q=%2Fm%2F09gbxjr" target="_blank">Google Trends</a> 可以看出来，在过去 5 年，Go 的热度始终在上升。通过以下内容，我们可以快速了解一下 Go 语言的基础特性，然后来决定是否深入地学习它。

## 变量定义

Go 可以使用 `var` 关键字来定义一个变量，类型放在变量名后面。如：

```go
// 定义一个变量
var a string

// 定义多个变量
var a, b string

// 定义多个变量并赋值
var a, b string = "a", "b"

// 变量具有初始值时可以省略类型
var a, b = "a", "b"
```

在**函数**中，可以在类型明确的地方使用短变量声明。例：

```go
func main() {

	a, b := "a", "b"

	// ...
}
```

使用 `const` 关键字来定义一个常量。例：

```go
const Pi = 3.14
```

## 类型系统

Go 的基本类型如下：

- bool
- string
- int int8 int16 int32 int64
- uint uint8 uint16 uint32 uint64 uintptr
- byte
- rune
- float32 float64
- complex64 complex128

其中，`int` 和 `uint` 在 32 位操作系统上是 32 位，在 64 位操作系统上是 64 位。

`uintptr` 是一个 `uint`，用于存放指针。

`byte` 是 `unit8` 的别名。

`rune` 是一个 `int32`，用于存放 Unicode 码点。(实际上 `rune` 相当于 C 中的 `char`，不过 `char` 存放的是 ASCII 码，因此只有 8 位。)

`complex64` 与 `complex128` 用于保存复数，实部与虚部分别由 `float32` 和 `float64` 组成。

未赋值的变量具有零值，对于数值类型来说是 `0`，布尔类型是 `false`，字符串类型为空字符串`""`。

表达式 T(v) 可以将值 v 强制转换为类型 T。如：

```go
a := 1.5
var b int = int(a) // b == 1
```

Go 带有类型推导，在声明一个变量而不指定其类型时，变量的类型由右值推导得出。对于整型的数值常量，总是取 `int`。而浮点型数值常量，总是取高精度的 `float64` 与 `complex128`。

## 运算符

Go 有类似 C 语言的运算符。例：

```go
// 算数运算符
var a = 1
var b = 2
var c = 0

c = a + b
c = a - b
c = a * b
c = a / b
c = a % b
c++
c--

// 关系运算符
var d = false

d = a == b
d = a != b
d = a > b
d = a < b
d = a >= b
d = a <= b

// 逻辑运算符
var e = true
var f = false
var g = false

g = e && f
g = e || f
g = !(e || f)

// 位运算符
var h = 0x00
var i = 0xff
var j = 0x00

j = h & i
j = h | i
j = h ^ i
j = h << 2
j = i >> 2
```

## 控制流语句

Go 只有一种循环结构：`for` 循环。Go 中的 `for` 语句有个特点，`for` 后面的三个表达式不需要括号。如：

```go
// 一个标准形式的 for 循环
sum := 0
for i := 0; i < 10; i++ {
	sum += i
}
```

`for` 语句中的初始化语句声明与后置语句可以省略，如：

```go
// 省略了初始化语句和后置语句的 for 循环
sum := 0
i := 0
for i < 10 {
	sum += i
	i++
}
```

此时，`for` 语句实际上就是 `while`。
同时，`for`语句可以更进一步，直接省略循环条件。这个时候，`for` 语句就是无限循环。例：

```go
for {
	// ...
}
```

Go 中的 `if` 语句也类似 `for`,没有括号。例：

```go
if num < 0 {
	num = num * -1
}
```

类似的，`if` 语句也可以添加一条初始化语句。如：

```go
if negative := -1; num < 0 {
	num = num * negative
}
```

值得注意的一点是不论是 `for` 还是 `if` 的初始化语句中声明的变量，其作用域都局限在当前的块中，在外部无法访问。

Go 中的 `switch` 语句是一组 `if` 的简化写法，它会运行第一个值等于条件表达式的 `case` 语句，如果 `case` 语句不以 `fallthrough` 语句作为结束，则执行完 `case` 之后会直接退出，不再执行后续的 `case` 语句。同时，与 `for` 和 `if` 一样，`switch` 的条件表达式同样不需要括号，且允许插入一条初始化表达式。如：

```go
text := ""

switch day := 6; day {
case 1:
  text = "星期一"

case 2:
  text = "星期二"

// ...

default:
	text = ""
}
```

这里需要注意一点：case 表达式是惰性求值的。

如果省略 switch 语句的条件表达式语句，那么默认就是 `switch true`。

## 函数

Go 使用 `func` 来定义一个函数。例：

```go
// 一个普通的函数
func add(a int, b int) int {
	c := a + b
	return c
}

// 省略连续的相同类型参数的类型
func add(a, b int) int {
	c := a + b
	return c
}

// 返回值可以被命名
func add(a, b int) (c int) {
	c = a + b
	return
}

// 一次可以返回多个返回值
func swap(a, b int) (int, int) {
	return b, a
}
```

Go 的函数没有默认参数，但是支持可变长参数函数(JavaScript 中管这个叫做剩余参数)。如：

```go
func acc(len int, num ...int) int {
	sum := 0

	for i := 0; i < len; i++ {
		sum += num[i]
	}

	return sum
}

// 调用函数：
acc(9, 1, 2, 3, 4, 5, 6, 7, 8, 9) // 返回 45
```

Go 的函数支持递归（不支持<a href="https://en.wikipedia.org/wiki/Tail_call" target="_blank">尾调用</a>优化）。例：

```go
func fibonacci(i int) int {
	if i <= 0 {
		return 0
	}

	if i == 1 {
		return 1
	}

	return fibonacci(i-1) + fibonacci(i-2)
}
```

Go 的函数支持 lambda 表达式和闭包。例：

```go
package main

import (
	"fmt"
)

func main() {
	createCounter := func() func() int {
		c := 0
		return func() int {
			c++
			return c
		}
	}

	count := createCounter()

	fmt.Println(count()) // 1
	fmt.Println(count()) // 2
	fmt.Println(count()) // 3
}
```

## 指针

Go 拥有指针，指针保存了值的内存地址。

类型 \*T 是指向 T 类型值的指针。其零值为 `nil`。

通过 `&` 操作符取得指向其操作目标的指针。

通过 `*` 操作符取得指针的底层值。

这是一个指针操作的例子：

```go
var p *int

var num = 1

p = &num

*p = 0 // num == 0
```

## 面向对象

Go 没有类，但是有结构体。Go 中使用 type 关键字来定义一个自定义类型，因此可以使用 type 来定义一个结构体类型。例：

```go
// 通过 type 声明结构体
type Vertex struct {
	X int
	Y int
}

vertex := Vertex{1, 2}

// 通过字面量使用结构体
vertex2 := struct {
	X int
	Y int
}{1, 2}
```

使用点号来访问结构体字段，如 `vertex.x` 。

有一点需要注意：结构体在赋值的时候是值传递。因此，修改结构体的字段必须使用指针。为了方便起见，通过指针访问结构体的字段时，可以省略 `*` 操作符。例：

```go
vertex := struct {
	X int
	Y int
}{0, 0}

p := vertex
p.X = 1
p.Y = 1 // vertex: {0 0}  p: {1 1}

q := &vertex
(*q).X = 2
(*q).Y = 2 // vertex: {2 2}  q: {2 2}
// 可以简化为
// q.X = 2
// q.Y = 2
```

我们还可以给结构体定义方法。方法就是带有接收者的函数，接收者实质上也是函数的参数，表示使用这个方法的结构体。如：

```go
type Vertex struct {
	X, Y int
}

// 一个带有接收者的函数
func (v Vertex) scale(s int) (int, int) {
	return v.X * s, v.Y * s
}

vertex := Vertex{1, 2}
vertex.scale(5) // 调用一个方法

// 函数的等价实现 =>
func scaleFunc(v Vertex, s int) (int, int) {
	return v.X * s, v.Y * s
}
scaleFunc(vertex, 5) // 调用一个函数
```

接收者同样也是值传递，如果在方法中需要改变结构体的值，则需要使用指针接收者。同样，为了方便起见，在使用指针接收者时，也可以省略 `*` 和 `&` 操作符。如：

```go
type Vertex struct {
	X, Y int
}

// 一个带有指针接收者的函数
func (v *Vertex) scale(s int) {
	(*v).X *= s
	(*v).Y *= s
	// 可以简化为
  // v.X *= s
  // v.Y *= s
}

vertex := Vertex{1, 2}
(&vertex).scale(5) // 传递指针接收者
// 可以简化为
// vertex.scale(5)

// 函数的等价实现 =>
func scaleFunc(v *Vertex, s int) {
	(*v).X *= s
	(*v).Y *= s
	// 可以简化为
  // v.X *= s
  // v.Y *= s
}

scaleFunc(&vertex, 5) // 作为函数参数而非接收者传入时，不能省略 `&` 操作符
```

虽然说 Go 中没有类，但是 Go 提供了接口。

接口是一组方法签名定义的集合，同样是一种类型。因此，依然使用 `type` 关键字来定义接口。接口类型的变量可以保存任何实现了这些方法的值。类型通过实现一个接口的所有方法来实现该接口，不需要 `implements` 关键字（隐式接口实现，相当于鸭子类型。），因此接口的定义与实现完全解耦，更加的灵活。例：

```go
// 定义一个接口，接口具有 scale 方法
type Scaler interface {
	scale(s int)
}

type Vertex struct {
	X, Y int
}

// Vertex 具有 scale 方法，因此隐式实现了这个接口
func (v *Vertex) scale(s int) {
	v.X *= s
	v.Y *= s
}

//
var scaler Scaler = &Vertex{1, 2} // 不能是 Vertex{1, 2} ，因为方法 scale 是为指针类型 *Vertex 定义的，所以值类型 Vertex{1, 2} 没有实现这个接口
```

一个接口类型的值在内部可以看做包含具体的值和值的类型的元组。比如上面这个例子中，接口的具体的值就是 `&Vertex{1, 2}`，而值的类型就是 `*Vertex`。在接口值调用方法时会执行其底层类型的同名方法。

当接口具体的值是 `nil` 时，方法仍然会被调用。这在其它一些语言中，会触发空指针异常。但是在 Go 中不会。为什么呢？因为接口值本身不是 nil，而方法实际上只是带有接收者的函数，因此当接口的具体值是 `nil` 时，方法依然可以调用，只是接收者的值为 `nil`，空指针异常会在方法内部被触发。与此同时，我们就可以在方法内部捕获空指针引用，避免错误。如：

```go
type Scaler interface {
	scale(s int)
}

type Vertex struct {
	X, Y int
}

func (v *Vertex) scale(s int) {
	if v == nil { // 当 v 是 nil 时跳出，避免空指针引用。
		return
	}
	v.X *= s
	v.Y *= s
}

var vertex *Vertex // 指针类型的零值是 nil

var scaler Scaler = vertex

scaler.scale(5) // scaler 本身不为 nil，不会触发空指针引用
```

需要注意的一点是，当接口值本身为 nil 时，内部既没有保存具体的值，也没有保存具体的类型，因此进行方法调用时无法找到的函数具体调用，从而引发空指针异常。

不声明任何方法的空接口可以保存任何类型的值（类似 typescript 中的 any 类型），空接口可以用来处理未知类型的值。Go 还给接口值提供了类型断言的语法，用于判断一个接口值是否保存了某个类型的值。类型断言会返回两个值，第一个值是接口保存的具体的值，第二个值是报告断言是否成功的布尔值。如果类型断言失败且没有读取第二个值则会触发异常。例：

```go
var a interface{} = "void interface"

b := a.(string) // b == "void interface"

c, ok := a.(int) // c == 0, ok == false

d := a.(int) // 触发异常
```

空接口可以结合类型选择的语法，依据传入的类型执行不同的语句。如：

```go
package main

import "fmt"

func checkType(x interface{}) {
	switch value := x.(type) { // .(type) 的类型选择语法只能在 switch 中使用
	case int:
		fmt.Println("Type is int: ", value)
	case string:
		fmt.Println("Type is string: ", value)
	default:
		fmt.Println("Unknow type: ", value)
	}
}

func main() {
	checkType(0)
	checkType("string")
	checkType(nil)
}
```

## 数组及映射

待续。

## 并发与异步

待续。

## 异常处理

待续。