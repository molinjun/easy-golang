# Beego 快速入门

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



