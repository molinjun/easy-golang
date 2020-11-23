# module

## GOPATH

Go 安装完成之后，有几个比较重要的环境变量：

- GOPATH: 工作目录
- GOROOT： GO 开发包的安装目录
- GOBIN： 编译器和连接器的安装位置

可以通过 `go env`命令来查看。GOPATH 默认在 $HOME/go。



## GOPATH 的工程目录

使用GOPATH的工作目录代码在 $GOPATH/src 目录下。go build 、go install 等产生的二进制文件会放在 $GOPATH/bin 目录，中间缓存文件会在 $GOPATH/pkg 目录下。使用方法如下：

- 将当前工作目录添加到GOPATH

  ```bash
  export GOPATH=`pwd`
  ```

- 建立 GOPATH 的源码目录

  创建 src 目录，并在src目录下创建源码目录，如 demo。

  ```bash
  mkdir -p src/hello
  ```

- 编译及运行

  ```bash
  go install demo
  ```

  此时会在 $GOPATH/bin 目录下生成可执行文件 demo。

使用 GOPATH 比较麻烦，特别是对于多项目工程。所以后面引入了 go module。



## Go module

Go 1.11 之后，推出了 Go modules，它允许在 GOPATH 目录以外来创建工程。

> 模块是相关Go包的集合。modules是源代码交换和版本控制的单元。 go命令直接支持使用modules，包括记录和解析对其他模块的依赖性。

要使用 Module，需要设置 `GO111MODULE`环境变量，有三个可选值：

- off: 关闭 module功能，沿用 GOPATH 模式
- on: 使用 modules，不依照 GOPATH 查找包
- auto: 默认值，根据当前目录是否决定使用module 功能。
  - 当前目录包含 go.mod 文件

> Module 启用后，依赖包安装位置为 $GOPATH/pkg



### go mod 指令

go mod 指令可以用来管理包：

- Go mod init : 目录初始化mod
- go mod download：下载依赖包
- go mod tidy: 移除不用的，拉取缺少的模块



## 参考

- [go mod 使用](https://juejin.im/post/6844903798658301960)
- [Introduction to Go Modules](https://roberto.selbach.ca/intro-to-go-modules/)
- [Go语言之依赖管理](https://www.liwenzhou.com/posts/Go/go_dependency/)