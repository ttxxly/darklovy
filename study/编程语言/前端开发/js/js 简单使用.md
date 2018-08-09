JavaScript 是世界流行的编程语言。 这门语言可用于 HTML 和 web， JavaScript 是脚本语言。JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。

HTML 中的脚本必须位于 `<script>` 与 `</script>` 标签之间。脚本可被放置在 html 页面的 `<body>` 和`<head>`部分中。

#### js 组成部分

	ECMAScript：语法
	BOM：浏览器对象模型
	DOM：文档对象模型
#### HTML 和 js 整合

* 方式一：在 html 页面中

```
<script></script>
```

* 方式二：外部的 js 文件

```
<script src=""></script>
```

在 html 页面中插入 JavaScript， 就需要使用 `<script>` 标签。

JavaScript 是所有现代浏览器以及 HTML5 中的默认脚本语言。

下面展示几个小例子：

##### 案例一

```
<!DOCTYPE html>
<html>
<body>
.
.
<script>
document.write("<h1>This is a heading</h1>");
document.write("<p>This is a paragraph</p>");
</script>
.
.
</body>
</html>
```

##### 实例二: 

```
<!DOCTYPE html>
<html>

<head>
<script>
function myFunction()
{
document.getElementById("demo").innerHTML="My First JavaScript Function";
}
</script>
</head>

<body>

<h1>My Web Page</h1>

<p id="demo">A Paragraph</p>

<button type="button" onclick="myFunction()">Try it</button>

</body>
</html>

```

##### 实例三

```
<!DOCTYPE html>
<html>
<body>

<h1>My Web Page</h1>

<p id="demo">A Paragraph</p>

<button type="button" onclick="myFunction()">Try it</button>

<script>
function myFunction()
{
document.getElementById("demo").innerHTML="My First JavaScript Function";
}
</script>

</body>
</html>

```

##### 案例四 

```
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
</body>
</html>
```

提示：外部脚本不能包含 `<script>` 标签。

