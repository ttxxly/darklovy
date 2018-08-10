```
常见的项目发布方式：（虚拟目录映射）

方式一：将项目放到 tomcat/webapps 文件下
方式二：修改 tomcat/conf/server.xml 
	大概130行：
		在 host 标签下，添加如下的代码：
			<Context path="/项目名" docBase="项目的磁盘目录"/>
		例如：
			<Context path="/myweb" docBase="F:\myweb"/>
方式三：
	在 tomcat/conf/引擎目录(Catalina)/主机目录下 新建一个 xml 文件
		文件的名称就是项目名 文件的内容如下：
			<Context docBase="F:\myweb"/>
			
方式四：通过 eclipse 发布项目
```

