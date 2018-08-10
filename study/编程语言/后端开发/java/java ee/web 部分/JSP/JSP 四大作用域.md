```
page：在本页中有效，跳出页面则失效；
request：跨页面作用，一般都是用于表单提交等；
session：在一定会话期间使用；
application：总是有效，关闭服务器后失效；
```

#### session的生存周期

```
session 的生存周期在不同的脚本运行环境下默认设置是不一样的.

    PHP 和 .NET 的默认 session 是20分钟
    ASP 的 session 是 10分钟
    JSP 是30分钟
    
在默认情况下，用户在关闭网页后，session 就已经失效了.
在实际的操作中，session 一般都被网站设计者限定了有效时间，比如常见的登陆时勾选的“保持登陆xx时间”

```

#### 相关面试题

```
1. Web程序中，当前用户上下文信息应该保存在下面哪个对象中（C）
  A page
  B request
  C session
  D Application
  解析：
  	当前用户上下文信息：session
    appication:当前应用
    pageContext：当前页面
    request:当前请求
```

