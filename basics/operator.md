# 运算符
`运算符（Operators）`是一些特殊符号，用好进行算术或者逻辑运算。操作符处理的值，叫做`操作数（Operand）`。
```go
a = 1 + 2
```
其中 `1` 和 `2` 为操作数，`+` 为运算符。

## 算术运算符
算术运算符用来进行算术运算，如加、减、乘、除和取余等。
```go
package main
import "fmt"

func main() {
  x, y := 5, 2

  // 加 +
  fmt.Printf("x + y = %d\n", x+y) // x + y = 7
  // 减 -
  fmt.Printf("x - y = %d\n", x-y) // x + y = 3
  // 乘 *
  fmt.Printf("x * y = %d\n", x*y) // x * y = 10
  // 整除 /
  fmt.Printf("x / y = %d\n", x/y) // x / y = 2
  // 取余 %
  fmt.Printf("x %% y = %d\n", x%y) // x % y = 1
  // 自增 ++
  x++                       // 相当于 x = x + 1
  fmt.Printf("x = %d\n", x) // x = 6
  // 自减 --
  x--                       // 相当于 x = x - 1
  fmt.Printf("x = %d\n", x) // x = 5
}
```
注意：Go 语言中，自增和自减不能用来给变量赋值，也没有 `++x`，和 C 语言不一样。
```go
c = x++  // syntax error: unexpected ++ at end of statement
```
## 关系运算符
比较运算符，用来比较两个值，返回 `true` 或 `false`。
```go
package main

import "fmt"

func main() {
  // 大于 >
  fmt.Println(5 > 2) // true

  // 大于等于 >=
  fmt.Println(5 >= 2) // true

  // 小于 <
  fmt.Println(5 < 2) // false

   // 小于等于 <=
   fmt.Println(5 <= 2) // false

  // 等于 ==
  fmt.Println(5 == 2) // false

  // 不等于 !=
  fmt.Println(5 != 2) // true
}s
```
## 逻辑运算符
逻辑运算符，用于逻辑计算，包括`与`、`或`和`非`三个运算符。
- `&&`: 与，两个操作数都为真，则为 true，否则为 false
- `||`: 或，两个操作数至少有一个为 true，则为true, 否则为 false
- `!`: 非，取反。操作数为真值，则为 true，否则为 false

```go
package main

import "fmt"

func main() {
	x, y := true, false

	fmt.Println(x && y) // false
	fmt.Println(x || y) // true
	fmt.Println(!x)     // false
}
```
注意，Go 语言中，非运算符 `!` 只能用在布尔类型的操作数上，其他类型会报错。 

## 位运算符
位运算符，用来将数字作为二进制数来按位操作。
- &: 按位与
- |：按位或
- ^: 按位异或，两位相异则为 1
- ~：按位取反。1变为0，0变为1
- <<: 左移，高位丢弃，低位补 0
- \>>: 右移

```go
package main

import "fmt"

func main() {
  x := 4  // 二进制  0000 0100
  y := 10 // 二进制 0000 1010

  fmt.Println(x & y)  // 0,  0000 0000
  fmt.Println(x | y)  // 14, 0000 1110
  fmt.Println(x ^ y)  // 14, 0000 1110
  fmt.Println(x >> 2) // 1,  0000 0001
  fmt.Println(x << 2) // 16, 0001 0000
}
```

## 赋值运算符
赋值运算符，用来给变量赋值。常用的赋值运算符为 `=`。
```python
a = 1
```
将值 1 赋值给变量 a。可以使用算术运算符、位运算符与 `=` 简写为组合赋值运算符。
```python
a = 1
a +=1 # 等同于 a = a + 1
```
## 其他运算符
还有两个比较重要的运算符 `&` 和 `*`。
- &：返回变量的内存地址
- \*：指针变量

```go
package main

import "fmt"

func main() {
  var i int = 3
  var ptr *int

  ptr = &i
  fmt.Printf("变量 i 的内存地址为 %d\n", ptr)
  fmt.Printf("变量 i 的值为 %d\n", *ptr)
}
```

## 运算符优先级
运算符优先级，是指当多个运算符存在是，优先哪种运算。下表列出了常用运算符的优先级：
| 优先级 | 运算符           |
| ------ | ---------------- |
| 5      | * / % << >> & &^ |
| 4      | + - \| ^         |
| 3      | == != < <= > >=  |
| 2      | &&               |
| 1      | \|\|             |

不过，为了增加可读性，通常建议多利用`小括号()` 来增加表达式的优先级。

