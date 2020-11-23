# GORM

[GORM](https://gorm.io/zh_CN/) 是一个 Golang 的 ORM 库。

## 安装

安装 gorm.

```bash
$ go get -u gorm.io/gorm
```

不同的数据库有不同的驱动。GORM 官方支持的数据库类型有： MySQL, PostgreSQL, SQlite, SQL Server。

```bash
# mysql
$ got get -u gorm.io/driver/mysql
```



## 连接数据库

使用 `DSN(Data Source Name， 数据源名称)`来连接数据库，格式如下：

```go
[username[:password]@][protocol[(address)]]/dbname[?param1=value1&...&paramN=valueN]
```

如，连接本地的 MySQL 数据库。

```go
dsn := "user:pass@tcp(127.0.0.1:3306)/dbname?charset=utf8mb4&parseTime=True&loc=Local"
```

连接数据库代码：

```go
// connect to mysql
dsn := "root:root123@tcp(127.0.0.1:3306)/demo?charset=utf8mb4&parseTime=True&loc=Local"
db, err := gorm.Open(mysql.Open(dsn), &gorm.Config{})
if err != nil {
	panic("Failed to connect database.")
}
```



