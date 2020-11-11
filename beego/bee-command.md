# bee 工具

bee 工具用来协助 beego 项目的开发，可以对 beego 项目进行创建、热编译、开发、测试和部署。

## 安装

通过如下指令安装 bee 工具：

```bash
$ go get github.com/beego/bee
```

默认安装在`$GOPATH/bin`里，需要将其添加到环境变量。

命令行输入命令`bee`,验证安装。

```bash
$ bee
Bee is a Fast and Flexible tool for managing your Beego Web Application.

USAGE
    bee command [arguments]

AVAILABLE COMMANDS

    version     Prints the current Bee version
    migrate     Runs database migrations
    api         Creates a Beego API application
    bale        Transforms non-Go files to Go source files
    fix         Fixes your application by making it compatible with newer versions of Beego
    pro         Source code generator
    dlv         Start a debugging session using Delve
    dockerize   Generates a Dockerfile for your Beego application
    generate    Source code generator
    hprose      Creates an RPC application based on Hprose and Beego frameworks
    new         Creates a Beego application
    pack        Compresses a Beego application into a single file
    rs          Run customized scripts
    run         Run the application by starting a local development server
    server      serving static content over HTTP on port

Use bee help [command] for more information about a command.
```

## 常见命令

### bee new 

`bee new <项目名>` 指令用来创建一个web项目。

### bee api

`bee api <项目名>` 用来创建一个 api 应用。目录结构如下：

```
apiproject
├── conf
│   └── app.conf
├── controllers
│   └── object.go
│   └── user.go
├── docs
│   └── doc.go
├── main.go
├── models
│   └── object.go
│   └── user.go
├── routers
│   └── router.go
└── tests
    └── default_test.go
```

### bee run

`bee run`命令用来监控 beego 项目，通过 fsnotify 监控文件系统，如果修改就热编译。

### bee pack

`bee pack`把项目打包成 zip 包，用来发布应用。

### bee dockerize

用来生成 Dockerfile 文件，实现 Docker 应用。如生成一个基于 1.6.4 Go版本环境为基础镜像的 Dockerfile， 并暴露 9000 端口。

```bash

```

