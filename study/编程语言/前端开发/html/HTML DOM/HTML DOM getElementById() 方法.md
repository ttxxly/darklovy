`getElementById()`方法可返回指定id的第一个对象的引用。

```
1. 格式
	document.getElementById(id)
	说明：通过id查找特定的元素。
		类似的方法还有：
			getElementByName()
			getElementsByTagName()
注：查找文档中的一个特定元素，最有效的办法是 getElementById()
```

#### 实例

```
1. 点击H1标签，弹窗 输出 H1标签内容
	<html>
    <head>
    <script type="text/javascript">
        function getValue()
        {
        var x=document.getElementById("myHeader")
        alert(x.innerHTML)
        }
    </script>
    </head>
    <body>

        <h1 id="myHeader" onclick="getValue()">This is a header</h1>
        <p>Click on the header to alert its value</p>

    </body>
    </html>
  2. 工具函数，方便使用
  	function id(x) {
      if (typeof x == "string") return document.getElementById(x);
      return x;
    }
```

