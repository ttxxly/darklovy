## value 属性

*value* 属性规定输入字段的初始值：

### 实例

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_attributes_value)

## readonly 属性

*readonly* 属性规定输入字段为只读（不能修改）：

### 实例

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" readonly>
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_attributes_readonly)

readonly 属性不需要值。它等同于 readonly="readonly"。

## disabled 属性

*disabled* 属性规定输入字段是禁用的。

被禁用的元素是不可用和不可点击的。

被禁用的元素不会被提交。

### 实例

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" disabled>
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_attributes_disabled)

disabled 属性不需要值。它等同于 disabled="disabled"。

## size 属性

*size* 属性规定输入字段的尺寸（以字符计）：

### 实例

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" size="40">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_attributes_size)

## maxlength 属性

*maxlength* 属性规定输入字段允许的最大长度：

### 实例

```
<form action="">
 First name:<br>
<input type="text" name="firstname" maxlength="10">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_input_attributes_maxlength)

如设置 maxlength 属性，则输入控件不会接受超过所允许数的字符。

该属性不会提供任何反馈。如果需要提醒用户，则必须编写 JavaScript 代码。

注释：输入限制并非万无一失。JavaScript 提供了很多方法来增加非法输入。如需安全地限制输入，则接受者（服务器）必须同时对限制进行检查。

## HTML5 属性

HTML5 为 <input> 增加了如下属性：

- autocomplete
- autofocus
- form
- formaction
- formenctype
- formmethod
- formnovalidate
- formtarget
- height 和 width
- list
- min 和 max
- multiple
- pattern (regexp)
- placeholder
- required
- step

并为 <form> 增加如需属性：

- autocomplete
- novalidate

## autocomplete 属性

autocomplete 属性规定表单或输入字段是否应该自动完成。

当自动完成开启，浏览器会基于用户之前的输入值自动填写值。

提示：您可以把表单的 autocomplete 设置为 on，同时把特定的输入字段设置为 off，反之亦然。

autocomplete 属性适用于 <form> 以及如下 <input> 类型：text、search、url、tel、email、password、datepickers、range 以及 color。

### 实例

自动完成开启的 HTML 表单（某个输入字段为 off）：

```
<form action="action_page.php" autocomplete="on">
   First name:<input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   E-mail: <input type="email" name="email" autocomplete="off"><br>
   <input type="submit">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_autocomplete)

提示：在某些浏览器中，您也许需要手动启用自动完成功能。

## novalidate 属性

novalidate 属性属于 <form> 属性。

如果设置，则 novalidate 规定在提交表单时不对表单数据进行验证。

### 实例

指示表单在被提交时不进行验证：

```
<form action="action_page.php" novalidate>
   E-mail: <input type="email" name="user_email">
   <input type="submit">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_form_novalidate)

## autofocus 属性

autofocus 属性是布尔属性。

如果设置，则规定当页面加载时 <input> 元素应该自动获得焦点。

### 实例

使 "First name" 输入字段在页面加载时自动获得焦点：

```
First name:<input type="text" name="fname" autofocus>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_autofocus)

## form 属性

form 属性规定 <input> 元素所属的一个或多个表单。

提示：如需引用一个以上的表单，请使用空格分隔的表单 id 列表。

### 实例

输入字段位于 HTML 表单之外（但仍属表单）：

```
<form action="action_page.php" id="form1">
   First name: <input type="text" name="fname"><br>
   <input type="submit" value="Submit">
</form>

 Last name: <input type="text" name="lname" form="form1">

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_form)

## formaction 属性

formaction 属性规定当提交表单时处理该输入控件的文件的 URL。

formaction 属性覆盖 <form> 元素的 action 属性。

formaction 属性适用于 type="submit" 以及 type="image"。

### 实例

拥有两个两个提交按钮并对于不同动作的 HTML 表单：

```
<form action="action_page.php">
   First name: <input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   <input type="submit" value="Submit"><br>
   <input type="submit" formaction="demo_admin.asp"
   value="Submit as admin">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_formaction)

## formenctype 属性

formenctype 属性规定当把表单数据（form-data）提交至服务器时如何对其进行编码（仅针对 method="post" 的表单）。

formenctype 属性覆盖 <form> 元素的 enctype 属性。

formenctype 属性适用于 type="submit" 以及 type="image"。

### 实例

发送默认编码以及编码为 "multipart/form-data"（第二个提交按钮）的表单数据（form-data）：

```
<form action="demo_post_enctype.asp" method="post">
   First name: <input type="text" name="fname"><br>
   <input type="submit" value="Submit">
   <input type="submit" formenctype="multipart/form-data"
   value="Submit as Multipart/form-data">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_formenctype)

## formmethod 属性

formmethod 属性定义用以向 action URL 发送表单数据（form-data）的 HTTP 方法。

formmethod 属性覆盖 <form> 元素的 method 属性。

formmethod 属性适用于 type="submit" 以及 type="image"。

### 实例

第二个提交按钮覆盖表单的 HTTP 方法：

```
<form action="action_page.php" method="get">
   First name: <input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   <input type="submit" value="Submit">
   <input type="submit" formmethod="post" formaction="demo_post.asp"
   value="Submit using POST">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_formmethod)

## formnovalidate 属性

novalidate 属性是布尔属性。

如果设置，则规定在提交表单时不对 <input> 元素进行验证。

formnovalidate 属性覆盖 <form> 元素的 novalidate 属性。

formnovalidate 属性可用于 type="submit"。

### 实例

拥有两个提交按钮的表单（验证和不验证）：

```
<form action="action_page.php">
   E-mail: <input type="email" name="userid"><br>
   <input type="submit" value="Submit"><br>
   <input type="submit" formnovalidate value="Submit without validation">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_formnovalidate)

## formtarget 属性

formtarget 属性规定的名称或关键词指示提交表单后在何处显示接收到的响应。

formtarget 属性会覆盖 <form> 元素的 target 属性。

formtarget 属性可与 type="submit" 和 type="image" 使用。

### 实例

这个表单有两个提交按钮，对应不同的目标窗口：

```
<form action="action_page.php">
   First name: <input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   <input type="submit" value="Submit as normal">
   <input type="submit" formtarget="_blank"
   value="Submit to a new window">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_formtarget)

## height 和 width 属性

height 和 width 属性规定 <input> 元素的高度和宽度。

height 和 width 属性仅用于 <input type="image">。

注释：请始终规定图像的尺寸。如果浏览器不清楚图像尺寸，则页面会在图像加载时闪烁。

### 实例

把图像定义为提交按钮，并设置 height 和 width 属性：

```
<input type="image" src="img_submit.gif" alt="Submit" width="48" height="48">
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_height_width)

## list 属性

list 属性引用的 <datalist> 元素中包含了 <input> 元素的预定义选项。

### 实例

使用 <datalist> 设置预定义值的 <input> 元素：

```
<input list="browsers">

<datalist id="browsers">
   <option value="Internet Explorer">
   <option value="Firefox">
   <option value="Chrome">
   <option value="Opera">
   <option value="Safari">
</datalist> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_datalist)

## min 和 max 属性

min 和 max 属性规定 <input> 元素的最小值和最大值。

min 和 max 属性适用于如需输入类型：number、range、date、datetime、datetime-local、month、time 以及 week。

### 实例

具有最小和最大值的 <input> 元素：

```
Enter a date before 1980-01-01:
<input type="date" name="bday" max="1979-12-31">

 Enter a date after 2000-01-01:
<input type="date" name="bday" min="2000-01-02">

 Quantity (between 1 and 5):
<input type="number" name="quantity" min="1" max="5">

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_max_min)

## multiple 属性

multiple 属性是布尔属性。

如果设置，则规定允许用户在 <input> 元素中输入一个以上的值。

multiple 属性适用于以下输入类型：email 和 file。

### 实例

接受多个值的文件上传字段：

```
Select images: <input type="file" name="img" multiple>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_multiple)

## pattern 属性

pattern 属性规定用于检查 <input> 元素值的正则表达式。

pattern 属性适用于以下输入类型：text、search、url、tel、email、and password。

提示：请使用全局的 title 属性对模式进行描述以帮助用户。

提示：请在我们的 JavaScript 教程中学习更多有关正则表达式的知识。

### 实例

只能包含三个字母的输入字段（无数字或特殊字符）：

```
Country code: 
<input type="text" name="country_code" pattern="[A-Za-z]{3}" title="Three letter country code">
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_pattern)

## placeholder 属性

placeholder 属性规定用以描述输入字段预期值的提示（样本值或有关格式的简短描述）。

该提示会在用户输入值之前显示在输入字段中。

placeholder 属性适用于以下输入类型：text、search、url、tel、email 以及 password。

### 实例

拥有占位符文本的输入字段：

```
<input type="text" name="fname" placeholder="First name">
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_placeholder)

## required 属性

required 属性是布尔属性。

如果设置，则规定在提交表单之前必须填写输入字段。

required 属性适用于以下输入类型：text、search、url、tel、email、password、date pickers、number、checkbox、radio、and file.

### 实例

必填的输入字段：

```
Username: <input type="text" name="usrname" required>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_required)

## step 属性

step 属性规定 <input> 元素的合法数字间隔。

示例：如果 step="3"，则合法数字应该是 -3、0、3、6、等等。

提示：step 属性可与 max 以及 min 属性一同使用，来创建合法值的范围。

step 属性适用于以下输入类型：number、range、date、datetime、datetime-local、month、time 以及 week。

### 示例

拥有具体的合法数字间隔的输入字段：

```
<input type="number" name="points" step="3">
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_input_step)