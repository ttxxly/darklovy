使用Servlet过滤器，需要在 `web.xml` 中配置

```
Servlet过滤器的配置包括两部分：
	第一部分是过滤器在Web应用中的定义:
		由<filter>元素表示，包括<filter-name>和<filter-class>两个必需的子元素
	第二部分是过滤器映射的定义:
		由<filter-mapping>元素表示.
		可以将一个过滤器映射到一个或者多个Servlet或JSP文件，
		也可以采用url-pattern将过滤器映射到任意特征的URL。
例子：
    <filter>  
        <filter-name>EncodingFilter</filter-name>  
        <filter-class>com.lessons.filter.EncodingFilter</filter-class>  
        <init-param>  
            <param-name>encoding</param-name>  
            <param-value>utf-8</param-value>  
        </init-param>//通过FilterConfig类的getInitParameter("paramName")  
    </filter>  
    <filter-mapping>  
        <filter-name>EncodingFilter</filter-name>  
        <url-pattern>/*</url-pattern>  
    </filter-mapping>  
```

发表于

* https://blog.csdn.net/jdliyao/article/details/79954265