# beego 简介

[Beego](https://beego.me/) 是一个用来构建并开发 Go 应用程序的开源 Web 框架。

## 架构

beego 是基于八大独立的模块构建的。

- cache: 缓存
- config：配置
- context
- httplibs
- logs：日志
- orm
- session
- toolbox

整体架构如下：

![img](https://beego.me/docs/images/architecture.png)

## 执行逻辑

beego 是一个典型的 MVC 架构，执行逻辑如下：

![img](https://beego.me/docs/images/flow.png)

## beego 项目结构

beego 项目的目录一般如下所示：

```
├── conf             // 配置
│   └── app.conf
├── controllers      // controller 目录
│   ├── admin
│   └── default.go
├── main.go          // 应用入口
├── models           // 定义model
│   └── models.go
├── static           // 静态文件
│   ├── css
│   ├── ico
│   ├── img
│   └── js
└── views             // 页面模板
    ├── admin
    └── index.tpl
```

