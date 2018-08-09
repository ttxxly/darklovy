style 属性用于改变 HTML 元素的样式。

#### style属性的作用

样式是HTML4引入的，它是一种新的首选的改变HTML元素的方式。通过使用style属性直接将样式添加到HTML元素，或者间接地在独立的样式表中（CSS文件）中定义。

#### 避免使用下面这些标签和属性

```
标签						描述
<center>	             定义居中的内容。
<font> 和 <basefont>	     定义 HTML 字体。
<s> 和 <strike>	         定义删除线文本
<u>	                      定义下划线文本

属性						  描述
align					定义文本的对齐方式
bgcolor					定义背景颜色
color					定义文本颜色
```

对于以上这些标签和属性：请使用样式来代替。

#### HTML 样式实例 - 背景颜色

background-color 属性为元素定义了背景颜色。

```
<html>

<body style="background-color:yellow">
<h2 style="background-color:red">This is a heading</h2>
<p style="background-color:green">This is a paragraph.</p>
</body>

</html>
```

#### HTML样式实例 - 字体、颜色和尺寸

font-family、color和font-size属性分别定义元素中文本的字体系列、颜色和字体大小。

```
<html>

<body>
<h1 style="font-family:verdana">A heading</h1>
<p style="font-family:arial;color:red;font-size:20px;">A paragraph.</p>
</body>

</html>
```

#### HTML 样式实例 - 文本对齐

text-align 属性规定了元素中文本的水平对齐方式：

```
<html>

<body>
<h1 style="text-align:center">This is a heading</h1>
<p>The heading above is aligned to the center of this page.</p>
</body>

</html>
```

