**HTML 表单用于搜集不同类型的用户输入。**

## <form> 元素

HTML 表单用于收集用户输入。

<form> 元素定义 HTML 表单：

### 实例

```
<form>
 .
form elements
 .
</form>

```

## HTML 表单包含*表单元素*。

表单元素指的是不同类型的 input 元素、复选框、单选按钮、提交按钮等等。

## <input> 元素

*<input>* 元素是最重要的*表单元素*。

<input> 元素有很多形态，根据不同的 *type* 属性。

这是本章中使用的类型：

| 类型     | 描述                 |
| ------ | ------------------ |
| text   | 定义常规文本输入。          |
| radio  | 定义单选按钮输入（选择多个选择之一） |
| submit | 定义提交按钮（提交表单）       |

注释：您稍后将在本教程学到更多有关输入类型的知识。

## 文本输入

*<input type="text">* 定义用于*文本输入*的单行输入字段：

### 实例

```
<form>
 First name:<br>
<input type="text" name="firstname">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_form_text)

在浏览器中看起来是这样的：

First name:
Last name:

注释：表单本身并不可见。还要注意文本字段的默认宽度是 20 个字符。

## 单选按钮输入

*<input type="radio">* 定义*单选按钮*。

单选按钮允许用户在有限数量的选项中选择其中之一：

### 实例

```
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_form_radio)

单选按钮在浏览器看起来是这样的：

Male 
Female

## 提交按钮

*<input type="submit">* 定义用于向*表单处理程序*（form-handler）*提交*表单的按钮。

表单处理程序通常是包含用来处理输入数据的脚本的服务器页面。

表单处理程序在表单的 *action* 属性中指定：

### 实例

```
<form action="action_page.php">
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_form_submit)

## Action 属性

*action 属性*定义在提交表单时执行的动作。

向服务器提交表单的通常做法是使用提交按钮。

通常，表单会被提交到 web 服务器上的网页。

在上面的例子中，指定了某个服务器脚本来处理被提交表单：

```
<form action="action_page.php">
```

如果省略 action 属性，则 action 会被设置为当前页面。

## Method 属性

*method 属性*规定在提交表单时所用的 HTTP 方法（*GET* 或 *POST*）：

```
<form action="action_page.php" method="GET">
```

或：

```
<form action="action_page.php" method="POST">
```

## 何时使用 GET？

您能够使用 GET（默认方法）：

如果表单提交是被动的（比如搜索引擎查询），并且没有敏感信息。

当您使用 GET 时，表单数据在页面地址栏中是可见的：

```
action_page.php?firstname=Mickey&lastname=Mouse
```

注释：GET 最适合少量数据的提交。浏览器会设定容量限制。

## 何时使用 POST？

您应该使用 POST：

如果表单正在更新数据，或者包含敏感信息（例如密码）。

POST 的安全性更加，因为在页面地址栏中被提交的数据是不可见的。

## Name 属性

如果要正确地被提交，每个输入字段必须设置一个 name 属性。

本例只会提交 "Last name" 输入字段：

### 实例

```
<form action="action_page.php">
First name:<br>
<input type="text" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_form_submit_id)

## 用 <fieldset> 组合表单数据

*<fieldset>* 元素组合表单中的相关数据

*<legend>* 元素为 <fieldset> 元素定义标题。

### 实例

```
<form action="action_page.php">
<fieldset>
<legend>Personal information:</legend>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit"></fieldset>
</form> 

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_form_legend)

## HTML Form 属性

HTML <form> 元素，已设置所有可能的属性，是这样的：

### 实例

```
<form action="action_page.php" method="GET" target="_blank" accept-charset="UTF-8"
ectype="application/x-www-form-urlencoded" autocomplete="off" novalidate>
.
form elements
 .
</form> 

```

下面是 <form> 属性的列表：

| 属性             | 描述                                       |
| -------------- | ---------------------------------------- |
| accept-charset | 规定在被提交表单中使用的字符集（默认：页面字符集）。               |
| action         | 规定向何处提交表单的地址（URL）（提交页面）。                 |
| autocomplete   | 规定浏览器应该自动完成表单（默认：开启）。                    |
| enctype        | 规定被提交数据的编码（默认：url-encoded）。              |
| method         | 规定在提交表单时所用的 HTTP 方法（默认：GET）。             |
| name           | 规定识别表单的名称（对于 DOM 使用：document.forms.name）。 |
| novalidate     | 规定浏览器不验证表单。                              |
| target         | 规定 action 属性中地址的目标（默认：_self）。            |