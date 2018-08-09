write方法可向文档写入 HTML 表达式或者 JavaScript 代码。

```
1. 格式：
	document.write(exp1,exp2,...)
2. 使用 write 方法的两种方式：
	(1) 在文档中使用该方法，输出 HTML
	(2) 在 调用该方法的窗口之外的窗口、床架中产生新文档。
		注意：务必使用 close() 关闭文档。
注：如果在文档已完成加载之后执行 document.write，整个 HTML 页面将被覆盖。
```

使用示例

```
1. 在浏览器中输出"Hello World!!!"(向输出流写文本)
	<html>
		<body>
			<script type="text/javascript">
				document.write("Hello World!!!!");
			</script>
		</body>
	</html>
2. 在浏览器中点击按钮输出"Hello World!!!"(向输出流写 HTML)
	<html>
    <head>
    <title>演示document.write输出html的用法</title>

    <script type="text/javascript">
        function RepeatWrite(){
            document.write("<p>Hello World!!!</p>")
        }
    </script> 
    </head>

    <body>
        <form>  
        <!--单击按钮调用写入函数-->  
        <input type="button" value="Replace Content" onClick="RepeatWrite()">  
      </form>  
    </body>
    </html>
    
```

