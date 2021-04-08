# 流程控制

## For 循环

Go 语言只有之中循环结构：`for 循环`。和其他语言一样，for 循环有三个部分，使用`分号`隔开。

- 初始语句：在第一次迭代中执行
- 条件表达式： 每次迭代都会执行
- 后置表达式：每次迭代的结束执行

初始化语句通常是一个缩写的变量声明语句`:=`，这个变量只在 for 循环中有效。条件表达式为 false 时，终止循环。

```go
package main

import "fmt"

func main() {
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}

	fmt.Println(sum)
}
```

初始化语句和后置表达式是可选的。Go 语言的 for 循环可以和其他语言的 while 循环一样使用。

```go
package main

import "fmt"

func main() {
	sum := 1
	for sum < 1000 {
		sum += sum
	}

	fmt.Println(sum)
}
```

如果省略循环条件，则是无限循环。

```go
package main

func main() {
	for {
	}
}
```

## If 语句

if 语句用于条件判断。Go 语言中 If 语句的条件表达式也不需要小括号。

```go
package main

import (
	"fmt"
	"math"
)

func sqrt(x float64) string {
	if x < 0 {
		return sqrt(-x) + "i"
	}
	return fmt.Sprint(math.Sqrt(x))
}
func main() {
	fmt.Println(sqrt(2), sqrt(-4))
}
```

可以在 if 语句的表达式中执行一个简单的赋值语句，该语句声明的变量只在 if 语句中有效。

```go
package main

import (
	"fmt"
	"math"
)

func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	}

	return lim
}
func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}
```

If .. else.. 语句和其他语言使用的方式一样。

```go
package main

import (
	"fmt"
	"math"
)

func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	} else {
		fmt.Printf("%g >= %g\n", v, lim)
	}

	return lim
}

func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}
```






>  需要注意的是，和别的语言不同，for 语句不需要加括号。