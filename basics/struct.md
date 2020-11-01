# 结构体 struct

数组只能存储同一种数据类型的数据，如果需要存储不同类型的数据，Go 语言可以使用`结构体 struct`。

## 定义结构体

结构体定义使用 `type`和`struct`关键字，格式为：

```go
type struct_variable_type struct {
  member definition;
   ...
   member definition;
}
```

相当于定义了一个新的数据类型，可以用来声明变量。

```go
variable_name := structure_variable_type {value1, value2...valuen}
```

访问结构体成员使用`.`，格式为`结构体.成员`。

```go
package main
import "fmt"
// 定义 student 结构体
type student struct {
	name string
	age  int
}

func main() {
  // 声明 student 类型的变量 student1
	var student1 student

  // 结构体成员赋值
	student1.name = "dennis"
	student1.age = 18
  
  // 访问结构体成员
	fmt.Printf("Student %s, age: %d\n", student1.name, student1.age)
}

```

## 结构体指针

结构体指针的定义和其他指针变量一致，格式为：

```go
var struct_pointer *结构体
```

改写以上程序：

```go
package main
import "fmt"

type student struct {
	name string
	age  int
}

func main() {
	var student1 student

	student1.name = "dennis"
	student1.age = 18

	var sPtr *student
	sPtr = &student1
	fmt.Printf("Student %s, age: %d\n", sPtr.name, sPtr.age)
}
```

## 函数方法（method）

`方法(Method)`是一种特殊的函数，它需要一个接受者。这个接受者可以是命名类型或者结构体类型的值或者指针。格式如下：

```go
func (variable_name variable_data_type) function_name() [return_type]{
   /* 函数体*/
}
```

举例：

```go
package main
import "fmt"

type student struct {
	name string
	age  int
}
// 定义 show 方法
func (stu *student) show() {
	fmt.Printf("Student %s, age: %d\n", stu.name, stu.age)
}

func main() {
	var student1 student

	student1.name = "dennis"
	student1.age = 18

	var sPtr *student = &student1
	sPtr.show()
}

```

