```
void init(ServletConfig config):初始化
	* 初始化方法
	* 执行者：服务器
	* 执行次数：一次
	* 执行时机：默认第一次访问的时候

void service(ServletRequest request, ServletResponse response):处理业务逻辑
	* 服务
	* 执行者：服务器
	* 执行次数：请求一次执行一次
	* 执行时机：请求来的时候

void destroy():销毁
	* 销毁
	* 执行者：服务器
	* 执行次数：只执行一次
	* 执行时机：当Servlet被移除的时候或者服务器正常关闭的时候
	
注意：Servlet是单实例多线程
	默认第一次访问的时候，服务器创建Servlet，并调用init实现初始化操作，并调用一次service方法
	每当请求的时候，服务器会创建一个县城，调用service方法执行自己的业务逻辑。
	当service被移除的时候服务器正常关闭的时候，服务器调用Servlet的destroy方法实现销毁操作。
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79949540