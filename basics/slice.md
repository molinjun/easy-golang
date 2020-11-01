# 切片 Slice

Go 数组的长度是固定的，很多场景都不太适用。Go 提供一种类似动态数组的内置类型`切片(Slice)`。切片可以追加元素，当切片的容量满了之后，会再次申请一块两倍容量的数组。

## 切片定义

### 声明

切片的声明和数组很相似，只是不指定长度，格式如下：

```go
var slice_name [] type
```

也可以通过 `make函数`来创建切片：

```go
make([]T, length, capacity)
```

其中，T 是数据类型，length是数组长度，capacity 是数组容量。capacity 是可选参数。

### 初始化

切片为初始话之前，默认为空切片`nil`，长度为0。切片的初始化和数组相似。

```go
package main
import "fmt"
func main() {
	var slice1 = []int{1, 2, 3}
  fmt.Println(slice1)     // Output: [1, 2, 3]

	slice2 := make([]int, 1, 2)
	slice2[0] = 1
  fmt.Println(slice2) // Output: [1]
}
```

通常的一种做法是，截取一个数组的片段来定义切片。格式为：

```go
数组名[起始索引：终止索引]
```

起始索引默认是第一个元素，终止索引默认是最后一个元素。

```go
package main
import "fmt"
func main() {
	var fruites = [4]string{"apple", "pear", "banana", "watermelon"}

	// 从第 3 个到倒数第 1 个
	s1 := fruites[2:] // [banana, watermelon]
	fmt.Println(s1)

	// 从第 1 个到第 2 个
	s2 := fruites[:2] // [apple, pear]
	fmt.Println(s2)
}

```

## 添加元素

切片可以通过`append()`动态添加元素。

```go
package main

import "fmt"

func main() {
	var fruits = []string{"apple", "banana"}

	fruits = append(fruits, "grape") // append 并不会修改原切片
  fmt.Println(fruits)  // Output: [apple banana grape]
}
```

注意，append 函数并不会更改原切片，所以需要将添加了新元素的切片重新赋值给原切片。

## 切片长度与容量

切片长度是指切片中元素的个数，通过函数`len()`获取。切片容量是指切片可以承载的元素个数，通过函数`cap()`获取。

```go
package main

import "fmt"

func main() {
	numbers := []int{1, 2}
	fmt.Printf("len= %d, cap=%d\n", len(numbers), cap(numbers))

	numbers = append(numbers, 3)
	fmt.Printf("len= %d, cap=%d\n", len(numbers), cap(numbers))

	numbers = append(numbers, 4)
	numbers = append(numbers, 5)
	fmt.Printf("len= %d, cap=%d\n", len(numbers), cap(numbers))
}
/* Output:
len= 2, cap=2
len= 3, cap=4
len= 5, cap=8
*/
```

可见，切片的容量随着元素的增加是成倍增长的。每当原切片满了之后，添加新元素，就会申请一块 2 倍容量的切片。

## 遍历

Go 语言中使用 range 来对数组和切片进行遍历。Range 表达式返回两个值，第一个值为索引，第二个值为元素值。

```go
package main
import "fmt"
func main() {
	nums := []int{1, 2, 3, 4, 5}
	sum := 0
  // 求元素的和
	for _, num := range nums {
		sum += num
	}
	fmt.Println("Sum:", sum)
}
// Output: Sum: 15
```



