```
myweb(项目名称)
	|
	| --- HTML css js image等目录或文件
	|
	| --- WEB-INF(特点：通过浏览器直接访问不到 目录)
	|		|
	|		| -- lib(项目存放的第三方 jar 包)
	|		| --- classes（存放的是我们自定义的java文件生成的 .class文件）
	|		| --- web.xml (当前项目的核心配置文件)
	|		|
发布方式：
	将项目放在webapps下
访问路径：
	http://主机:端口号/项目名称/资源路径
	例如：我的项目 myweb
		资源：myweb 有一个 1.html
	http:localhost:80/myweb/1.html
```

