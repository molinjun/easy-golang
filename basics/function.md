# 函数

`函数`是用来执行某个`指定任务`的代码块。Go 标准库提供了丰富的内置函数。也可以自己定义不同功能的函数。

## 函数定义

函数声明要指定`函数名称`、`返回类型`和`参数`。函数使用关键字`func`声明，格式如下：

```go
func function_name( [parameter list] ) [return_types] {
   函数体
}
```

函数定义解析：

- func: 函数使用关键字 func 声明。
- function_name: 函数名称。
- Parameter list: 参数列表指定参数的类型、顺序以及个数。函数声明的参数叫做`形参`，实际调用函数传的值为`实参`。函数也可以不需要参数。
- return_types: 返回值类型。特别注意，Go 语言支持多返回值。
- 函数体：函数的实现逻辑。

来个例子，定义一个两个数求和的函数。

```go
package main

import "fmt"

func add(num1 int, num2 int) int {
  sum := num1 + num2
  return sum
}

func main() {
	a, b := 1, 2

	sum := add(a, b)
	fmt.Printf("%d + %d = %d\n", a, b, sum)
}
// 输出: 1 + 2 = 3
```

## 函数参数

函数定义时，参数列表中的参数，叫做`形参`。形参相当于是定义在函数体内的局部变量，仅函数体内可以访问。调用函数时，实际传入的参数的值，叫做`实参`。
参数传递通常有两种方式：

- 值传递：调用函数时，将`实参复制一份传递给函数`。函数对参数的操作，不影响原参数值。
- 引用传递：调用函数时，将`实参的地址传递给函数`。函数对参数的操作，会影响原参数的值。

稍微有点绕，举个例子：

**值传递**

```go
package main

import "fmt"

func swap(a, b int) int {
	var temp int

	temp = a
	a = b
	b = a

	return temp
}

func main() {
	var a int = 1
	var b int = 2

	fmt.Printf("交换前：a = %d, b = %d\n", a, b)
	swap(a, b)
	fmt.Printf("交换后：a = %d, b = %d\n", a, b)
}
/* output:
交换前：a = 1, b = 2
交换后：a = 1, b = 2
*/
```

**引用传递**

```go
package main

import "fmt"

func swap(x, y *int) int {
	var temp int

	temp = *x
	*x = *y
	*y = temp

	return temp
}

func main() {
	var a int = 1
	var b int = 2

	fmt.Printf("交换前：a = %d, b = %d\n", a, b)
	swap(&a, &b)
	fmt.Printf("交换后：a = %d, b = %d\n", a, b)
}
/* output:
交换前：a = 1, b = 2
交换后：a = 2, b = 1
*/
```



## 返回值

Go 函数可以返回多个值：

```go
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}
func main() {
	a, b := "Hello", "World"

	a, b = swap(a, b)
	fmt.Println(a, b)
}
// 输出：World Hello
```

## 