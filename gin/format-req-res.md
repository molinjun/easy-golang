# 格式化请求体和响应体

我们通常需要对请求体或者响应体做一个格式化，限制请求的参数并且规范响应的内容。

## 请求体格式化

前面我们使用 `PostFrom()`和 `DefaultPostForm()`来获取表单数据，但是都需要一个个属性去获取，当属性比较多时，就显得很冗余。这就需要使用 Gin 框架的实体绑定功能，它可以将表单数据与定义结构体绑定。

以一个用户注册功能为例，我们需要两个参数：`phone` 和 `password`。我们定义一个 RegisterInfo 的结构体：

```go

```

常用的 bind 方法有：

- ShouldBindQuery(): 用于 GET 请求绑定 query 参数
- ShouldBind(): 用于 POST 请求数据的绑定
- ShouldBindJson(): 对JSON 数据进行绑定，并自动解析

### ShouldBindQuery

以一个用户注册功能为例，我们需要两个参数：`phone` 和 `password`。

```go
package main

import (
	"fmt"
	"log"

	"github.com/gin-gonic/gin"
)
// 定义请求结构体
type GetUserInfo struct {
	Username string `form:"name"`
	Phone    string `form:"phone"`
}

func main() {
	engine := gin.Default()

	engine.GET("/userinfo", func(context *gin.Context) {
		var requestInfo GetUserInfo
		if err := context.ShouldBindQuery(&requestInfo); err != nil {
			log.Fatal(err.Error())
		}
		fmt.Println(requestInfo)
		context.JSON(200, gin.H{
			"username": requestInfo.Username,
			"phone":    requestInfo.Phone,
		})
	})

	engine.Run(":8090")
}

```

Postman 请求测试：

<img src="/Users/dennisge/Library/Application Support/typora-user-images/image-20201112181341698.png" alt="image-20201112181341698" style="zoom: 50%;" />

### ShouldBind

这种方式支持 `x-www-form-urlencoded` 和 `application/json`。

定义结构体：

```go
type RegisterInfo struct {
	Username string `form:"username"`
	Phone    string `form:"phone"`
	Password string `form:"password"`
}
```

添加路由：

```go
	engine.POST("/register", func(c *gin.Context) {
		var registerInfo RegisterInfo
		if err := c.ShouldBind(&registerInfo); err != nil {
			log.Fatal(err.Error())
		}
		fmt.Println(registerInfo)
		c.JSON(200, gin.H{
			"username": registerInfo.Username,
			"phone":    registerInfo.Phone,
		})
	})
```

Postman 请求测试：

<img src="/Users/dennisge/Library/Application Support/typora-user-images/image-20201112182551373.png" alt="image-20201112182551373" style="zoom:50%;" />

### ShouldBindJson 和 BindJson

ShouldBindJson 和 ShouldBind 类似，只是不支持 `x-www-url-encoded` 只支持`applicaton/json`。改写入行程序如下：

```go
package main

import (
	"fmt"
	"log"

	"github.com/gin-gonic/gin"
)

// 定义请求结构体
type GetUserInfo struct {
	Username string `form:"name"`
	Phone    string `form:"phone"`
}

type RegisterInfo struct {
	Username string `form:"username"`
	Phone    string `form:"phone"`
	Password string `form:"password"`
}

func main() {
	engine := gin.Default()

	engine.GET("/userinfo", func(context *gin.Context) {
		var requestInfo GetUserInfo
		if err := context.ShouldBindQuery(&requestInfo); err != nil {
			log.Fatal(err.Error())
		}
		context.JSON(200, gin.H{
			"username": requestInfo.Username,
			"phone":    requestInfo.Phone,
		})
	})

	engine.POST("/register", func(c *gin.Context) {
		var registerInfo RegisterInfo
		if err := c.BindJSON(&registerInfo); err != nil {
			c.JSON(400, gin.H{
				"messaege": "invalid post body",
			})
			return
		}
		c.JSON(200, gin.H{
			"username": registerInfo.Username,
			"phone":    registerInfo.Phone,
		})
	})
	engine.Run(":8090")
}
```



## 响应体格式化

Gin框架支持多种响应体的格式：

- []byte
- string
- Map 
- 结构体
- html 模板
- 静态资源

### []byte

可以通过 context.Writer.Write 方法来写入 []byte 数据来响应。添加路由如下：

```go
	engine.GET("/check", func(c *gin.Context) {
		var message string = "Server is working"
		c.Writer.Write([]byte(message))
	}
```

请求测试：

![image-20201112185003533](/Users/dennisge/Library/Application Support/typora-user-images/image-20201112185003533.png)

Writer 是 Gin 框架封装的一个 ResponseWriter 接口类型。write  方法其实是用的内置的 http.ResponseWrite的write 方法。

### string

正如上面说的，Gin 的 ResponseWriter 封装了一个 WriteString 的方法来返回string。我们可以给些上面的代码。

```go
	engine.GET("/check", func(c *gin.Context) {
		var message string = "Server is working"
		c.Writer.WriteString(message)
	}
```



### JSON

实际项目开发中，我们普遍使用 JSON。`context.JSON()`方法可以将结构体类型的数据转换成为 JSON 格式的数据。

**map 类型**

可以使用map 类型来返回，如下：

```go
	engine.GET("/check", func(c *gin.Context) {
		var message string = "Server is working"
		c.JSON(200, map[string]interface{}{
			"code":    0,
			"message": message,
		})
```

**结构体**

使用map还是不够方便，我们通常使用结构体来规范返回体。定义返回体：

```go
type Response struct {
	Code    int         `json:"code"`
	Message string      `json:"message"`
	Data    interface{} `json:"data"`
}
```

修改 check 处理函数。

```go
engine.GET("/check", func(c *gin.Context) {
		var message string = "Server is working"
		res := &Response{
			Code:    1,
			Message: message,
		}
		c.JSON(200, res)
	})
```

Postman 请求测试：

![image-20201112191112397](/Users/dennisge/Library/Application Support/typora-user-images/image-20201112191112397.png)

## 完整代码

```go
package main

import (
	"fmt"
	"log"

	"github.com/gin-gonic/gin"
)

// 定义请求结构体
type GetUserInfo struct {
	Username string `form:"name"`
	Phone    string `form:"phone"`
}

type RegisterInfo struct {
	Username string `form:"username"`
	Phone    string `form:"phone"`
	Password string `form:"password"`
}

type Response struct {
	Code    int         `json:"code"`
	Message string      `json:"message"`
	Data    interface{} `json:"data"`
}

func main() {
	engine := gin.Default()

	engine.GET("/userinfo", func(context *gin.Context) {
		var requestInfo GetUserInfo
		if err := context.ShouldBindQuery(&requestInfo); err != nil {
			log.Fatal(err.Error())
		}
		fmt.Println(requestInfo)
		context.JSON(200, gin.H{
			"username": requestInfo.Username,
			"phone":    requestInfo.Phone,
		})
	})

	engine.POST("/register", func(c *gin.Context) {
		var registerInfo RegisterInfo
		if err := c.BindJSON(&registerInfo); err != nil {
			c.JSON(400, gin.H{
				"messaege": "invalid post body",
			})
			return
		}
		fmt.Println(registerInfo)
		c.JSON(200, gin.H{
			"username": registerInfo.Username,
			"phone":    registerInfo.Phone,
		})
	})

	engine.GET("/check", func(c *gin.Context) {
		var message string = "Server is working"
		res := &Response{
			Code:    1,
			Message: message,
		}
		c.JSON(200, res)
	})

	engine.Run(":8090")
}

```

