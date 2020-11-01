# Map (集合)

Map 是一种无序的键值对的集合。Map 可以通过键值 key 快速检索的数据。

## 定义 Map

Go 语言使用`map`关键字来声明 Map。

```go
var map_varialbe map[key_data_type]value_data_type
```

未初始化的 map 是一个 nil map，不能存放键值对，需要使用 make 函数来进行初始化。

```go
map_variable = make(map[key_data_type]value_data_type)
```

通常合并在一起：

```go
map_variable := make(map[key_data_type]value_data_type)
```

如定义一个 scoreMap, key为string类型的姓名, value 为 int 类型的分数。 

```
	scoreMap := make(map[string]int)
```

## 添加键值

对于定义好的 map，可以插入键值对。使用`map名称["键名"]`的格式。

```go
scoreMap["dennis"] = 90
```

## 遍历

map 也是使用 range 来进行遍历。range 第一个返回的是 key, 第二个是 value。

```go
for index, value := range scoreMap {
  // 处理元素
}
```

## 判断元素是否存在

Go 语言中 if 表达式不能做空值判断，只能判断布尔值。但是map 表达式通常会返回第二参数，表明元素是否存在（true/false）。

```go
if score, ok := scoreMap["dennis"]; ok {
  fmt.Println("Score of dennis is ", score)
} else {
  fmt.Println("No score of dennis")
}
```

## 删除键值

可以通过 delete 函数删除 map 中的键值。

```go
delete(scoreMap, "dennis") // 删除 scoreMap 中 key 为 dennis 的键值对
```

## 例子

```go
package main
import "fmt"

func main() {
	// 定义 map
	scoreMap := make(map[string]int)

	// 添加键值对
	scoreMap["dennis"] = 99
	scoreMap["andy"] = 85

	// 遍历
	for name, score := range scoreMap {
		fmt.Println(name, score)
	}

	// 判断元素存在
	if score, ok := scoreMap["dennis"]; ok {
		fmt.Println("Score of dennis is ", score)
	} else {
		fmt.Println("No score of dennis")
	}

	// 删除元素
	delete(scoreMap, "andy")
	fmt.Println(scoreMap)
}
```

