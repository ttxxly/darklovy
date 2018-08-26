JavaWeb三大组件指的是：Servlet、Filter、Listener，这三个组件在JavaWeb开发中分别提供不同的功能.

#### Servlet

```
Servlet：
	用于处理客户端请求的动态资源。
	当我们在浏览器中键入一个地址回车跳转后，请求就会被发送到对应的Servlet上进行处理。
	Servlet的任务有：
		1. 接收请求数据：客户端请求会被封装成HttpServletRequest对象
			里面包含了请求头、参数等各种信息。
		2. 处理请求：通常我们会在service、doPost或者doGet方法进行接收参数，
			并且调用业务层(service)的方法来处理请求。
		3. 完成相应：处理完请求后，一般会转发(forward)或者重定向(redirect)到某个页面
			转发是HttpServletRequest中的方法，重定向是HttpServletResponse中的方法。
	Servlet的创建：
		Servlet可以在第一次接收请求时被创建，也可以在服务器启动时就被创建，只需要在
			web.xml中配置。
		配置信息如下：
			<load-on-startup>5</load-on-startup>
			说明：
				值>=0 时：表示容器在应用启动时就加在这个Servlet
				值<0或者没有指定时，表示容器在该Servlet被请求时才加载。
	Servlet中常见的方法：
		1. void init(ServletConfig)
			Servlet初始化方法，只在创建Servlet实例的时候调用一次，Servlet是单例的。
			整个服务器就只创建一个同类型Servlet.
		2. void service(ServletRequest,ServletResponse)
			Servlet的处理请求方法，在Servlet被请求时会马上被调用。
			每处理一次请求，就会被调用一次。
			ServletRequest类为请求类，ServletResponse类为响应类。
		3. void destory()
			Servlet销毁之前执行的方法，只执行一次，用于释放Servlet占有的资源。
			通常Servlet没有什么可要释放的，所以该方法一般是空的。
		4. ServletConfig getServletConfig()
			获取Servlet的配置信息的方法。
			配置信息就是WEB-INF目录下的web.xml中的Servlet标签里面的信息。
		5. String getServletInfo()
			获取Servlet的信息的方法。
	Servlet的配置示例：
        <servlet>
            <servlet-name>LoginServlet</servlet-name>
            <servlet-class>com.briup.servlet.LoginServlet</servlet-class>
        </servlet>
        <servlet-mapping>
            <servlet-name>LoginServlet</servlet-name>
            <url-pattern>/login</url-pattern>
        </servlet-mapping>
```

#### Filter

```
Filter:
	主要负责拦截请求和放行。
	filter四种拦截方式
        REQUEST：
        	直接访问目标资源时执行过滤器。
        	包括：在地址栏中直接访问、表单提交、超链接、重定向，
        	只要在地址栏中可以看到目标资源的路径，就是REQUEST；
        FORWARD：
            转发访问执行过滤器。
            包括RequestDispatcher#forward()方法、< jsp:forward>标签都是转发访问；
        INCLUDE：
        	包含访问执行过滤器。
        	包括RequestDispatcher#include()方法、
        	< jsp:include>标签都是包含访问；
        ERROR：
        	当目标资源在web.xml中配置为< error-page>中时，
        	并且真的出现了异常，转发到目标资源时，会执行过滤器。
    url-mapping的写法 
        匹配规则有三种：
            精确匹配 —— 如/foo.htm，只会匹配foo.htm这个URL
            路径匹配 —— 如/foo/*，会匹配以foo为前缀的URL
            后缀匹配 —— 如*.htm，会匹配所有以.htm为后缀的URL
        < url-pattern>的其他写法，如/foo/ ，/.htm ，/foo 都是不对的。
    执行filter的顺序 
		如果有多个过滤器都匹配该请求，顺序决定于web.xml filter-mapping的顺序，
		在前面的先执行，后面的后执行 
```

#### Listener

```
Listener:
	监听器。
```

