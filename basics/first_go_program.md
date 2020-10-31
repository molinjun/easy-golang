# 第一个 Go 程序

Go 语言的源文件，后缀名为 `.go`。在工作目录新建目录 `go-tutorial`，然后在目录下创建文件 `first.go`，输入如下代码：

```go
package main
import "fmt"

func main() {
	message := "Hello World!"
	fmt.Println(message) // 输出：Hello World!
}
```

下面简单看下这个程序的结构：

- 第一行 `package main` 定义了包名。每个 Go 源文件需要在非注释的第一行指明文件属于哪个包。package main 表示一个可执行的程序，每个 Go 程序都必须包含一个名为 `main` 的包。

- `import` 语句告知 Go 编译器引入包，这里需要引入 `fmt` 包。fmt 包实现了格式化 I/O 的函数，如这里的 `Println`。

- `func main()` 是程序开始执行的函数。每个函数都必须包含一个 main 函数。若没有 `init()` 函数，则先执行 main 函数。

- 接下来，定义一个变量 `message`，并赋值为 "Hello World!" 字符串

- `fmt.Println()` 将字符串输出到控制台。

- `// 语句`为注释，增加程序的可读性

输入代码保存后，在命令行执行以下命令：

```bash
$ go run first.go
Hello World!
```

`go run` 为 Go 指令，用于执行 Go 程序。也可以使用 `go build` 指令生成二进制文件，再执行。

```bash
$ go build first.go
$ ./first
Hello World!
```

