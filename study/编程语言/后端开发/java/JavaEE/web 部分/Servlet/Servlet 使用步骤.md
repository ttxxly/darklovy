```
1. 编写一个servlet的步骤：
    1. 编写一个类
        a. 继承 HttpServlet
        b. 重写doGET或者doPost方法
    2. 编写配置文件(WEB-INF/web.xml)
        a. 注册 Servlet
            servlet-name：给Servlet起个名字 全局唯一
            servlet-class：保存servlet的全限定名 复制过来就好
        b. 绑定路径
            servlet-name：使用上面已起好的名字
            url-pattern:访问路径 目前必须以"/"开头 唯一
    3. 访问
        HTTP://主机：端口号/项目名/路径
2. 接收参数： key=value
	String value = request.getParameter("key");
	例如：http://localhost/day09/hello?username=tom
		request.getParameter("username");就可以获取到值
3. 向浏览器回写内容
	resp.setContentType("text/html;charset=utf-8");
	resp.getWriter().print("数据:"+value);
```

#### 相关问题

```
1. HttpServlet 无法导包问题
	选中当前项目，右键选择 Build Path -> Configure Build Path
	找到 Libraries -> Add Libray 选择 Server RunTime 
	在选中配置好的服务器 finish
```

