```
组成部分：
	请求行 请求头 请求体

	请求行：请求信息的第一行
		格式：请求方式	访问的资源	协议/版本
		例如：GET	/day0801/1.html	HTTP/1.1
		请求方式：get 和 post
			get会把参数放在 url 后面 post 不会
			get参数大小有限制，post请求没有限制
			get请求没有请求体 post请求有请求体，请求参数放在请求体中
	请求头：请求信息的第二行到空行结束
		格式：key/value (value 可以是多个值)
		常见的请求头：
			Accept: text/html,image/*		--支持数据类型
			Accept-Charset: ISO-8859-1	--字符集
			Accept-Encoding: gzip		--支持压缩
			Accept-Language:zh-cn 		--语言环境
			Host: www.itcast.cn:80		--访问主机
			If-Modified-Since: Tue, 11 Jul 2000 18:23:51 GMT	  --缓存文件的最后修改时间
			Referer: http://www.itcast.com/index.jsp	 --来自哪个页面、防盗链
			User-Agent: Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)
			Cookie
			Connection: close/Keep-Alive   	--链接状态
			Date: Tue, 11 Jul 2000 18:23:51 GMT	--时间
			
	请求体：空行以下的内容
		只有 post 才有请求体 get请求参数 http://xxxx?username=tom&password=123
		格式：usename=tom&password=123
```

