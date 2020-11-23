# 容器化部署

## 代码运行

代码

```go
package main

import (
	"fmt"
	"net/http"
)

func check(w http.ResponseWriter, _ *http.Request) {
	_, _ = w.Write([]byte("Hello Golang!"))
}
func main() {
	http.HandleFunc("/check", check)
	server := &http.Server{
		Addr: ":8090",
	}
	fmt.Println("Server lift ...")
	if err := server.ListenAndServe(); err != nil {
		fmt.Printf("Server lift failed with err:%v\n", err)
	}
}
```

访问：

```bash
$ curl localhost:8090/check
Hello Golang!%     
```

## Docker 构建

Dockerfile 如下：

```dockerfile
FROM golang:alpine

# 为我们的镜像设置必要的环境变量
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

# 移动到工作目录：/build
WORKDIR /build

# 将代码复制到容器中
COPY . .

# 将我们的代码编译成二进制可执行文件app
RUN go build -o app .

# 移动到用于存放生成的二进制文件的 /dist 目录
WORKDIR /dist

# 将二进制文件从 /build 目录复制到这里
RUN cp /build/app .

# 声明服务端口
EXPOSE 8090

# 启动容器时运行的命令
CMD ["/dist/app"]
```

构建镜像

```bash
docker build -t goweb_demo .
```

运行

```bash
 docker run --name goweb_demo -p 8090:8090 goweb_demo
```



## 分阶段构建

上面构建的镜像达到200多兆，但其实我们只需要把可执行文件放在最终镜像中就可以。Dockerfile 如下：

```dockerfile
FROM golang:alpine AS builder

# 为我们的镜像设置必要的环境变量
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

# 移动到工作目录：/build
WORKDIR /build

# 将代码复制到容器中
COPY . .

# 将我们的代码编译成二进制可执行文件 app
RUN go build -o app .

###################
# 接下来创建一个小镜像
###################
FROM scratch

# 从builder镜像中把/dist/app 拷贝到当前目录
COPY --from=builder /build/app /

# 需要运行的命令
ENTRYPOINT ["/app"]
```

新生成的镜像只有几兆。

## 参考

- [如何使用Docker部署Go Web应用](https://www.liwenzhou.com/posts/Go/how_to_deploy_go_app_using_docker/)