![img](http://img.my.csdn.net/uploads/201210/23/1350993311_7168.png)

HttpServlet中的doGet()和doPost()由service()方法根据提交请求的方式(GET/POST)来调用。默认为GET

	体系结构：
	    Servlet:接口
	        |
	    GenericServlet:抽象类
	        |
	    HttpServlet:抽象类
	        |
	    自定义servlet
	    
	servlet常用方法:
		void init(ServletConfig config):初始化
		void service(ServletRequest request,ServletResponse response):服务 处理业务逻辑
		void destroy():销毁
		
		ServletConfig getServletConfig() :获取当前servlet的配置对象
	
	GenericServlet常用方法:	
		除了service方法没有显示,其他都实现了
		空参的Init() 若我们自己想对servlet进行初始化操作,重写这个init()方法即可
	
	HttpServlet常用方法：
		service做了实现，把参数强转，调用了重载的service方法
			重载的service方法获取请求的方式,根据请求方式的不同调用相应doXxx()方法
		doGet和doPost方法