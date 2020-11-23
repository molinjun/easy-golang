## 基本结构

### 目录结构：

- config: 配置
- router: 路由配置及路由的中间件（鉴权、日志、异常捕获）
- middleware: 中间件 
- controller: 控制层，验证提交数据，传递给 service
- service: 业务逻辑层，专注业务逻辑，不操作数据库
- repository: 数据库操作，多表操作，与业务无关
- model: 数据库的 ORM
- entity 响应数据的结构体， controller 请求体验证结构体
- proto: gRPC的 *.pb.go
- util: 通用工具函数
- test: 测试

### 架构图：

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9nbzlqcEczQnVoVFhOOVk0WUEwN283ZDRDWW5WbmJ3R05lVUJaRzBEbk9nUXE0ZzVwQXpVMjlQdUVoa2I0d1YyR1ZVQ21CaWNtSUFqR2liV3pydWNPN3h3LzY0MD93eF9mbXQ9cG5n?x-oss-process=image/format,png)

### 工具

- 日志： [zerolog](https://github.com/rs/zerolog)
- 配置：[viper](https://github.com/spf13/viper)
- Redis: [redigo](https://github.com/gomodule/redigo)
- ORM: [gorm](https://github.com/go-gorm/gorm)
- 定时任务：[cron](https://github.com/robfig/cron)
- 参数校验：[Validator](https://github.com/go-playground/validator)
- 

