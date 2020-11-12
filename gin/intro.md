# Gin

[Gin](https://gin-gonic.com/) 是一个用 Go 编写的 HTTP web 框架。

**特点**

- 快速：基于 Radix 树的路由，小内存占用，没有反射
- 中间件：Logger，Authorization等
- 自动恢复：可以 catch HTTP  请求的 panic，并恢复
- JSON 验证

## 快速入门

## 安装

Gin 要求 Go 1.9 及以上版本。下载并安装 gin:

```bash
$ go get -u github.com/gin-gonic/gin
```

代码中使用：

```go
import "github.com/gin-gonic/gin"
```

创建工作目录，并初始化目录：

```bash
$ mkdir demo
$ cd demo
$ git mod init demo
```

新建一个 文件 `main.go`，输入一下内容：

```go
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()

	r.GET("/", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "Hello World",
		})
	})

	// 默认监听并在 0.0.0.0:8080 上启动服务
	r.Run()
}
```

运行代码。

```bash
go run main.go
```

开发过程中，我们需要热更新。可以使用以下工具：[air](https://github.com/cosmtrek/air) 和 [bee](https://github.com/beego/bee)。bee 是 beego的工具，不过也可以使用于 gin 框架。

此时在访问 `http://127.0.0.1:8080`。

```bash
$ curl http://127.0.0.1:8080
{"message":"Hello World"}%
```