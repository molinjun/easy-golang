# Go 开发环境搭建



在开始语法学习之前，我们需要搭建好 Go 的开发环境。

> 如果不想搭建本地开发环境，建议使用[在线编辑环境 repl.it](https://repl.it/languages/go)，支持代码编辑、运行以及智能提示，还支持 vim 的按键模式。

下面介绍一下 Go 的本地开发环境搭建。
## Go 安装
Go 的安装非常简单，建议查看[官网安装说明 https://golang.org/doc/install](https://golang.org/doc/install) 。下面将简单介绍 Go 在 macOS、Linux 和 Windows 下的安装。
>随着版本更新，以下安装步骤可能有调整，具体以官网为准。笔者行文时的版本是 **go1.15**。

首先在官网 [https://golang.org/dl/](https://golang.org/dl/) 下载相应的 Go 版本。

- Apple macOS:   https://golang.org/dl/go1.15.3.darwin-amd64.pkg
- Linux: https://golang.org/dl/go1.15.3.linux-amd64.tar.gz
- Windows: https://golang.org/dl/go1.15.3.windows-amd64.msi

macOS 系统默认安装在 `/usr/local/go`，Windows 安装在 `C:\Go`。

### macOS
双击下载的 `.pkg` 文件安装即可。默认安装在 `/usr/local/go` 目录，并且自动添加 `/usr/local/go/bin`到 PATH 路径。重启命令行窗口即可生效。

### Windows
打开下载的 `.msi` 文件安装。默认安装在 `C:\Go` 目录，并将 Go 命令添加到 PATH 路径。重启命令行窗口即可生效。
### Linux

将下载的压缩包解压到 `/usr/local`目录，程序安装目录为`/usr/local/go`。

```bash
tar -C /usr/local -xzf go1.15.3.linux-amd64.tar.gz
```

添加目录 `/usr/local/go/bin` 到 PATH 环境变量。打开 $HOME/.profile 文件，最后一样添加：

```shell
export PATH=$PATH:/usr/local/go/bin
```

保存文件，并重新打开命令行窗口生效。

### 验证安装

验证安装成功，打开命令行工具：

```bash
$ go version
go version go1.15.3 darwin/amd64
```

## VSCode 编辑器

文本编辑器的种类很多，大家可以任意选择一款自己顺手的编辑器。这里笔者选择现在用的比较多的 `VSCode`。VSCode 免费、轻量，并且拥有丰富的插件。VSCode 同时支 持 Windows、Linux 和 macOS，并且安装特别简单。大家可以到[官网下载页](https://code.visualstudio.com/download)自行下载安装。

安装完 VSCode之后，安装`插件 Go`。它能对 Go 程序进行语法检测以及提供智能提示。安装方法如下：

<img src="https://cdn.jsdelivr.net/gh/gedennis/file@main/images/vscode-for-golang.png?width=" alt="VSCode 安装 Go 插件" style="zoom: 35%;" />

## 卸载

如果需要卸载 Go，可以按照下面的步骤完成。

**Linux/macOS**

- 删除 Go 目录 `/usr/local/go` 。
- macOS 系统需要删除 `/etc/paths.d/go` 文件。

```bash
$ sudo rm -rf /usr/local/go
$ sudo rm -rf /etc/paths.d/go  #just for macOS
```
然后删除所有与 Go 有关的环境变量，可能在 `.bash_profile` 文件或者 `.zshrc` 文件。

**Windows**
Windows 下，通过`【控制面板】` -> `添加/删除程序`，选择 Go 完成卸载即可。

## 总结

这一小节介绍了 Go 在不同操作系统 macOS、Linux 和 Windows 下的开发环境搭建。

- Go 的安装卸载。
- VSCode 的安装及 Go 插件安装。

## 参考

- [https://golang.org/doc/install](https://golang.org/doc/install)
- [https://golang.org/doc/manage-install](https://golang.org/doc/manage-install)

