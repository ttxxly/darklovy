```
响应的组成部分：
	响应行	响应头	响应体
响应行：响应信息的第一行
	格式：协议/版本 状态码 状态码说明
	例如： HTTP/1.1 200 OK 
	状态码：
		200	正常响应成功 
		302 重定向
		304 读缓存
		404 用户操作资源不存在
		500 服务器内部异常
响应头：从响应信息的第二行到空行结束
	格式： key/value (value可以是多个值)
	常见的头：
        Location: http://www.it315.org/index.jsp 	--跳转方向
        Server:apache tomcat			--服务器型号
        Content-Encoding: gzip 			--数据压缩
        Content-Length: 80 			--数据长度
        Content-Language: zh-cn 		--语言环境
        Content-Type: text/html; charset=GB2312 		--数据类型
        Last-Modified: Tue, 11 Jul 2000 18:23:51 GMT	--最后修改时间
        Refresh: 1;url=http://www.it315.org		--定时刷新
        Content-Disposition: attachment; filename=aaa.zip	--下载
        Set-Cookie:SS=Q0=5Lb_nQ; path=/search
        Expires: -1					--缓存
        Cache-Control: no-cache  			--缓存
        Pragma: no-cache   				--缓存
        Connection: close/Keep-Alive   			--连接
        Date: Tue, 11 Jul 2000 18:23:51 GMT
响应体：空行以下的信息
	页面上展示的信息
```

