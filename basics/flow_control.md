# 流程控制语句

流程控制语句，通常包括`条件判断语句` 和 `循环语句`。
## 条件判断
条件判断语句，用来根据不同的条件，执行不同的操作。一般的格式为：
- if 语句
```go
if 布尔表达式 {
    /* 布尔表达式为 true 时执行 */
}
```
- if...else 语句
```go
if 布尔表达式 {
    /* 布尔表达式为 true 时执行 */
} else {
    /* 布尔表达式为 true 时执行 */
}
// 多个条件分支
if 布尔表达式1 {
    /* 布尔表达式为 true 时执行 */
} else if 布尔表达式2 {
    /* 布尔表达式1 为 false,
       布尔表达式2 为 true,
    时执行 */
} else {
   // 两个表达式都为 false 时执行
}
```
- switch 语句
switch 语句用于基于不同的条件执行不同动作，每个 case 分支都是唯一的。switch 语句从上至下，直到找到匹配项。
```go
switch variable {
    case val1:
        ...
    case val2:
        ...
    default:
        ...
}
```
变量 `variable` 可以使任意类型，值 val1 和 val2 必须是同类型的值。
```go
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var grade string = "B"
   var marks int = 90

   switch marks {
      case 90: grade = "A"
      case 80: grade = "B"
      case 50,60,70 : grade = "C"
      default: grade = "D"  
   }

   switch {
      case grade == "A" :
         fmt.Printf("优秀!\n" )    
      case grade == "B", grade == "C" :
         fmt.Printf("良好\n" )      
      case grade == "D" :
         fmt.Printf("及格\n" )      
      case grade == "F":
         fmt.Printf("不及格\n" )
      default:
         fmt.Printf("差\n" );
   }
   fmt.Printf("你的等级是 %s\n", grade );      
}
```
Go 语言中匹配项默认带 break 语句，匹配成功之后不会执行其他 case。如果需要执行后续语句，可以使用 `fallthrough`。
```go
package main

import "fmt"

func main() {

    switch {
    case false:
            fmt.Println("1、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("2、case 条件语句为 true")
            fallthrough
    case false:
            fmt.Println("3、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("4、case 条件语句为 true")
    case false:
            fmt.Println("5、case 条件语句为 false")
            fallthrough
    default:
            fmt.Println("6、默认 case")
    }
}
```
## 循环语句
循环语句，用来执行有规律的重复操作。Go 语言中只有 `for` 循环，没有 `while` 循环。for 语句的格式为：
```go
for init; condition; post {
    /* 循环体 */
}
```
- init：初始条件，给控制变量赋初值
- condition: 关系或逻辑表达式，循环控制条件
- post：给控制变量或减量
执行的流程：
- 首先，执行init 语句，进行初始化。
- 判断循环条件，若为真，执行循环体语句。
- 执行 post 语句，更新控制变量
- 继续判断循环条件，若为假，退出 for 循环

for 循环的 range 格式可以对 slice、map、数组、字符串等进行迭代循环。格式如下：
```go
for key, value := range oldMap {
    newMap[key] = value
}
```
Go 语言虽然没有 `while` 语句，但可以通过 for 语句实现，只要省略 init 语句和 post 语句。
```go
package main

import "fmt"

func main() {

	sum := 0
	i := 1
	for i <= 10 {
		sum += i
		i++
	}

	fmt.Println(sum) // 55
}
```