# 网络请求处理

## 创建 Engine

Engine 是一个结构体，代表 gin 框架的一个实例，包含路由组、中间件、页面渲染接口、框架配置等内容。可以使用两种方式创建：

- gin.Default()
- gin.New()

gin.Default() 底层也是使用 gin.New()，但是会加上 Logger 和 Recover 中间件。

- Logger : 负责输出日志
- Recovery: 程序 panic中断了，会自动恢复程序执行。

通常，我们选择使用 `gin.Default()`来创建。

```go
engine = gin.Default()
```

Engine 中有 RouterGroup（路由集合），定义如下：

```go
type RouterGroup struct {
    Handlers HandlersChain
    basePath string
    engine   *Engine
    root     bool
}
```

RouterGroup 用来对 http 请求进行解析，并制定相应的处理函数。下面介绍几种对于 HTTP 请求处理的方法。

## 处理 HTTP 请求

HTTP 请求有很多种的请求方法，如常用的：GET、POST、POST 和 PUT 等。Engine 使用内置了很多种方法来处理不同类型的 HTTP 请求。

### Handle() 方法

可以直接使用 `Handle方法`来处理 HTTP 请求，如下：

```go
engine.Hanlde(httpMethod, relativePath, handlers)
```

- httpMethod: 请求类型，如GET、POST、DELETE
- relativePath: 请求路径
- Handlers: 处理函数，格式为：`func(c *gin.Context){}`。

#### GET 请求

例如增加一个路由 `/hello`。

```go
	engine.Handle("GET", "/hello", func(c *gin.Context) {
		// 获取 query 参数
		name := c.DefaultQuery("name", "nobody")

		c.JSON(200, gin.H{
			"message": "Hello " + name,
		})
	}
```

Context 是gin 框架内的一个结构体，代表请求的上下文。我们可以通过它获取请求的参数以及返回响应数据。

- c.DefaultQuery(param, defaultValue): 获取query中的某个属性，可设置默认值
- c.JSON(code, body): 返回一个json响应

验证请求：

```bash
$ curl http://127.0.0.1:8090/hello\?name\=dennis
{"message":"Hello dennis"}%
```

#### POST  请求

添加一个 `/login` 路径，如下所示：

```go
engine.Handle("POST", "/login", func(c *gin.Context) {
		// 获取 body 参数
		username := c.PostForm("username")
		password := c.PostForm("password")
		fmt.Println(username, password)
		if username != "dennis" || password != "123" {
			c.JSON(400, gin.H{
				"message": "login failed",
			})
			return
		}
		c.JSON(200, gin.H{
			"message": "login success",
		})
	})
```

这里使用 `PostForm()`来获取 Form 表单的参数。请求如下：

![image-20201112170414945](/Users/dennisge/Library/Application Support/typora-user-images/image-20201112170414945.png)

注意这里的 Content-Type 是 `x-www-form-urlencoded`，PostForm 不能获取 `application/json`的body数据。

### engine.[method] 方法

 常用的有：

- engine.GET()
- engine.POST()
- egine.DELETE()

简单来说，就是把 Handle 方法的第一个参数 httpMethod 通过另外一个方式调用。改写上面的程序如下：

```go
package main

import (
	"github.com/gin-gonic/gin"
)

func main() {
	engine := gin.Default()
	// GET
	engine.GET("/hello", func(c *gin.Context) {
		// 获取 query 参数
		name := c.Query("name")

		c.JSON(200, gin.H{
			"message": "Hello " + name,
		})
	})
  // POST
	engine.POST("/login", func(c *gin.Context) {
		// 获取 body 参数
		username, usernameExists := c.GetPostForm("username")
		password, passwordExits := c.GetPostForm("password")

		if !usernameExists || !passwordExits {
			c.JSON(400, gin.H{
				"message": "Invalid params",
			})
			return
		}
		if username != "dennis" || password != "123" {
			c.JSON(400, gin.H{
				"message": "login failed",
			})
			return
		}
		c.JSON(200, gin.H{
			"message": "login success",
		})
	})
	// 监听0.0.0.0:8090 上启动服务,默认为8080
	engine.Run(":8090")
}

```

这里我们用了另外两种方式来获取请求参数。

- context.Query()： 和 context.DefaultQuery 类似，只是不能提供默认值
- context.GetPostForm(): 和 context.PostForm()类似，只是返回值带了第二个参数，一个bool 值判断参数是否存在。