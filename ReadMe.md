## Sino.Extensions.Dapper
用Dapper提供MySQL数据仓储的默认实现    

[![Build status](https://ci.appveyor.com/api/projects/status/o4y6ne8ix0tot0vq?svg=true)](https://ci.appveyor.com/project/vip56/sino-extensions-dapper)
[![NuGet](https://img.shields.io/nuget/v/Nuget.Core.svg?style=plastic)](https://www.nuget.org/packages/Sino.Extensions.Dapper)

## 使用方式
```
Install-Package Sino.Extensions.Dapper
```

在`Startup`中进行配置，增加用于读和写的MySQL连接字符串
```
string readConStr = Configuration.GetConnectionString("ReadConnectionString");
string writeConStr = Configuration.GetConnectionString("WriteConnectionString");
services.AddDapper(writeConStr, readConStr);
```
  
为了保证了兼容性，所以`Connection`对象依然可以使用，但是对于特殊场景的使用可以直接使用`WriteConnection`或`ReadConnection`
来强制指定需要使用写数据库或读数据库。

## 其他
其中`Sino.Extensions.Dapper.UnitTest`项目中包含了如何使用`Dapper`实现多表查询等演示代码。   
因为`MySql.Data`官方库升级后默认使用SSL所以连接字符串中请放置`SslMode=none`    

虽然MySqlConnection使用了连接池的概念，但如果使用单例MySqlConnection对象在并发情况下会出现因为Driver属性赋值问题导致并发线程中仅有一个成功，其他线程会出现
重复使用Driver属性从而导致DataReader对象重复使用的问题。


## 版本更新记录  
* 2018.3.7 支持asp.net core 2.0 by y-z-f
* 2018.9.11 升级相关类库