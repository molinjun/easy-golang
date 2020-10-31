# 基础语法
上一章中，我们通过 `Hello World` 程序基本了解 Go 程序的基本结构。Go 程序是由一系列的标记组成的，如关键字、标识符、变量、字面量和符号等组成的。接下来我们将介绍 Go 语言的基本语法。
## 关键字与标识符
`关键字（Keywords）`，是 Go 语言本身用来定义语法和结构的保留字。Go 语言中有 25 个关键字（截止目前为止）。
```go
break	default	func	interface	select
case	defer	go	map	struct
chan	else	goto	package	switch
const	fallthrough	if	range	type
continue	for	import	return	var
```
以及 36 个预定义标识符：
```go
append	bool	byte	cap	close	complex	complex64	complex128	uint16
copy	false	float32	float64	imag	int	int8	int16	uint32
int32	int64	iota	len	make	new	nil	panic	uint64
print	println	real	recover	string	true	uint	uint8	uintptr
```

`标识符（Identifiers）`用来给变量、函数、或者类取名，例如示例程序中的 `message`。标识符有一定的命名规则：
- 由`字母`、`数字`和下划线 `_` 组成
- 首字母必须是字母或者下划线，不能是数字
- 标识符不能是关键字（keyword）

另外，Go 语言是大小写敏感的。`message` 和 `Message` 是两个不同的标识符。
> 建议标识符取更容易理解的单词，message 比 m 更容易让人理解。

## 语句与注释
`语句（Statement）`是编译器执行的一个单元，如示例程序中的 `message := "Hello World!"`，就是一个赋值语句。通常一个语句为一行。
Go 程序中，语句结尾不需要分号（;）。但如果把多个语句放在一行，需要用`分号隔开`。
```Go

```

`注释（Comments）`，用来描述程序的作用，增加程序的可读性。解释器执行程序的时候，会忽略注释。单行注释使用`//`，多行注释使用`/**/`。
```Go
/*
这是多行注释
*/

// 这是单行注释
```
## 字面量与变量
`字面量（Literal）`，表示固定不变的值。通常用来给变量赋值（位于赋值=右边），如：
```Python
a := 10
```
`10` 就是一个数值型字面量，用来给变量 `a` 赋值。Python 中有多种不同类型的字面量。
```Python
# 数值型字面量 Numberic Literal
100  # 整型字面量 Integer
3.14  # 浮点型字面量 Float

# 字符型字面量 String Literal
"Golang"  # 双引号

# 布尔值字面量 Boolean Literal
true  # True
false  # False
```
以上是常见的一些字面量类型，后续在数据类型章节再详细介绍。

`变量（Variable）`，实际上是内存的一个地址，用来存储数据。变量的声明用 `var` 关键字，格式如下：
```Go
var 变量名 数据类型
```
如，声明一个 int 类型的变量 a，同时定义两个 string 类型变量 str1 和 str2:
```go
var a int
var str1, str2 string
```
变量声明之后，需要对变量赋值，进行`初始化`。
```go
var num int // 声明变量
num = 10    // 初始化，赋值为 10
```
变量如果没有初始化，则默认为`零值`。各种类型的零值如下：
- 数值类型：0
- 布尔类型：false
- 字符串： ""(空字符串)
- 其他类型：nil

也可以不指定变量类型，自动根据值来判断类型。
```go
var num = 10
var str1, str2 = "hello", "hi"
```
可以通过 `:=` 简写为：
```go
num := 10
str1, str2 := "hello", "hi"
```
> 但`:=`这种简写格式，只能在函数体中有效。

可以通过 `&` 来获取变量的内存地址。
```go
package main

import "fmt"

func main() {
    a := 10
    fmt.Println("a 的内存地址：", &a)
}
// 输出：a 的内存地址： 0xc0000b4008
```
`常量`，是一种特殊的变量，它对应的值不可变。常量的数据类型可是布尔型、数字型（整数型、浮点型和复数型）和字符串型。格式为：
```go
const 常量名 [类型] = 值
```
常量通常使用`大写字母`来标识。
```go
const PI = 3.14
const APP_NAME = "demo"
```
常量还可以用作`枚举`：
```go
const (
    START = 0
    PAUSE = 1
    STOP  = 2
)
```