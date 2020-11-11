# Beego 快速入门

[Beego](https://beego.me/) 是一个用来构建并开发 Go 应用程序的开源 Web 框架。

## 环境搭建

- 配置环境变量。

```Bash
# 如果您还没添加 $GOPATH 变量
$ echo 'export GOPATH="$HOME/go"' >> ~/.zshrc # 您所使用的sh对应的配置文件

# 如果您已经添加了 $GOPATH 变量
$ echo 'export PATH="$GOPATH/bin:$PATH"' >> ~/.zshrc # 您所使用的sh对应的配置文件
$ source ~/.zshrc
```

- 安装包
```Bash
# 安装 beego
$ go get -u github.com/astaxie/beego 
# 安装 bee 工具
$ go get -u github.com/beego/bee
```

这里注意，有时候可能会安装 bee 会出错。需要设置`GO111MODULE`。

```bash
$ go env -w GO111MODULE=on
```

## 创建 beego 应用

在工作目录通过 `bee new` 命令创建项目 hello。

```bash
$ bee new hello
```

在 hello 目录下，通过 `bee run` 运行项目。

```bash
$ cd hello
$ bee run
```

启动之后，在浏览器中打开 http://localhost:8080/ 进行访问，可以看到如下欢迎画面。

<img src="https://cdn.jsdelivr.net/gh/gedennis/file@main/images/beego-welcome.png" style="zoom: 50%;" />

## 搭建一个简单的应用

下面我们创建一个简单的 Hello World 应用。在创建一个目录 demo 作为工作目录，然后初始化。

```go
$ mkdir demo
$ cd demo
$ go mod init demo
```

创建 `hello.go`文件，输入一下内容：

```go
package main

import (
	"github.com/astaxie/beego"
)

// controller
type MainController struct {
	beego.Controller
}

// method
func (this *MainController) Get() {
	this.Ctx.WriteString("Hello World")
}

func main() {
	// router
	beego.Router("/", &MainController{})

	// run application
	beego.Run()
}
```

**程序解释**

- 引入包`github.com/astaxie/beego`，beego包会初始化一个BeeApp 的应用和一些参数。
- 定义Controller: 利用 Go 语言的组合概念，MainController 匿名包含 beego.Controller，继承其方法。
- 定义 RESTful 方法：beego.Controller 中默认有Get、Post、Delete 和 Put等方法。根据需求重写相应方法。
- main 函数：应用的入口
- Router 注册路由：利用 Router 函数定义路由，两个参数：`路径`和`Controller 指针`。

**运行程序**

在工作目录编译并执行：

```bash
$ go build -o demo demo.go
$ ./demo
```

在浏览器输入 `http://127.0.0.1:8080`可以看到浏览器显示`Hello World`字符串。

