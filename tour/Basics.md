## Packages 包

每个 Go 程序都是由`包（Package）` 组成，并且由 `main` package 启动。程序中可以通过`import`关键字引入别的包。如下面的程序：

```go
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("My favorite Number is ", rand.Intn(10))
}
```

程序中引入了 `fmt` 和 `math/rand`两个包。通常，包的名称为引入包路径的最后一个元素，如示例中包的名字为 rand.

import 语句可以多行书写，也可以使用`单括号`包裹起来。

一个包导出的属性或函数需要`首字母大写`，首字母小写的元素不能被包外访问。如示例程序中 math 包的 Pi 值。

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Pi)
}
```

## 函数 Function

函数可以有0到多个参数，参数的类型在参数的后面。如下面的程序：

```go
package main

import "fmt"

func add(x int, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(42, 13))
}
```

如果参数类型相同，可以缩写。

```go
x int, y int
x, y int
```

Go 语言中的函数可以有多个返回值。

```go
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```

Go 语言可以给返回值命名，等同于在函数顶部定义的变量。这样函数中的 return 就可以不用带参数 了，叫做`naked return`。这种方式只建议用在短函数中，以免影响程序的可读性。

```go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	fmt.Println(split(17))
}
```

## 变量 Variables

Go 语言中使用关键字 `var` 来定义变量，变量的定义在语句的最后，格式如下：

```go
var 变量名 变量类型
```

变量声明的语句可以在 package 或 function 中。

```go
package main

import "fmt"

var c, python, java bool

func main() {
	var i int
	fmt.Println(i, c, python, java)
}
```

变量定义时可以带有初始化值。如果有初始值，可以省略变量定义的类型。

```go
package main

import "fmt"

var i, j int = 1, 2

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}
```

Go 语言中可以使用 `:=` 来简化变量的定义和初始化。

```go
package main

import "fmt"

func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"
	fmt.Println(i, j, k, c, python, java)
}
```

不过这种缩写的变量定义方式`只能使用在函数内部`。

## 基础数据类型 Basic Types

 Golang 的数据类型如下：

```go
bool
string

int int8 int16 int32 int64
uint uint8 uint16 uint32 uint64 uintptr

byte // uint8 的别称
rune // int32 的别称，代表一个 Unicode 码

float32 float64

complex64 complex128
```

int、uint 和 uintptr 通常根据系统来决定变量是 32 位还是 64 位。当需要一个定义一个整数变量，建议使用 int。

变量申明是没有定义会默认给一个初始化零值。

- 数据类型：0
- bool 类型：false
- String: 空字符串 “”

#### 类型转换

Go 语言可以通过`T(v)`的格式进行数据类型的转换。T 是需要转换的类型，v 是要转的的值。

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	var x, y int = 3, 4
	var f float64 = math.Sqrt(x*x + y*y)
	var z uint = uint(f)
	fmt.Println(x, y, z)
}
```

特别注意的是，Go 语言中没有隐式的类型转换，都需要显示转换。

#### 类型推断 Type inference

如果定义变量的时候没有显示的指定数据类型，Go 语言会根据右边的值进行类型推断，决定变量的数据类型。

```go
package main

import "fmt"

func main() {
	i := "Hello"
	fmt.Printf("Type is %T\n", i)
}
```

### 常量 Constants

Go 语言通过 `const`关键字来定义常量，但常量不可以使用 `:=` 语法。

```go
package main

import "fmt"

const Pi = 3.14

func main() {
	const World = "世界"
	fmt.Println("Hello", World)

	fmt.Println("Happy", Pi, "Day")

	const Truth = true
	fmt.Println("Go rules?", Truth)
}
```

数值常量是一个高精度值，一个无类型定义的常量根据上下文决定数据类型。int 类型最大存 64位的整型值。

