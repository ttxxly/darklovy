## 亲自试一试 - 实例

- [文档的标题](http://www.w3school.com.cn/tiy/t.asp?f=html_title)

  <title> 标题定义文档的标题。

- [所有链接一个目标](http://www.w3school.com.cn/tiy/t.asp?f=html_base)

  如何使用 base 标签使页面中的所有标签在新窗口中打开。

- [文档描述](http://www.w3school.com.cn/tiy/t.asp?f=html_meta)

  使用 <meta> 元素来描述文档。

- [文档关键词](http://www.w3school.com.cn/tiy/t.asp?f=html_keywords)

  使用 <meta> 元素来定义文档的关键词。

- [重定向用户](http://www.w3school.com.cn/tiy/t.asp?f=html_redirect)

  如何把用户重定向到新的网址。

## HTML <head> 元素

<head> 元素是所有头部元素的容器。<head> 内的元素可包含脚本，指示浏览器在何处可以找到样式表，提供元信息，等等。

以下标签都可以添加到 head 部分：<title>、<base>、<link>、<meta>、<script> 以及 <style>。

## HTML <title> 元素

<title> 标签定义文档的标题。

title 元素在所有 HTML/XHTML 文档中都是必需的。

title 元素能够：

- 定义浏览器工具栏中的标题
- 提供页面被添加到收藏夹时显示的标题
- 显示在搜索引擎结果中的页面标题

一个简化的 HTML 文档：

```
<!DOCTYPE html>
<html>
<head>
<title>Title of the document</title>
</head>

<body>
The content of the document......
</body>

</html>

```

## HTML <base> 元素

<base> 标签为页面上的所有链接规定默认地址或默认目标（target）：

```
<head>
<base href="http://www.w3school.com.cn/images/" />
<base target="_blank" />
</head>

```

## HTML <link> 元素

<link> 标签定义文档与外部资源之间的关系。

<link> 标签最常用于连接样式表：

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>

```

## HTML <style> 元素

<style> 标签用于为 HTML 文档定义样式信息。

您可以在 style 元素内规定 HTML 元素在浏览器中呈现的样式：

```
<head>
<style type="text/css">
body {background-color:yellow}
p {color:blue}
</style>
</head>

```

## HTML <meta> 元素

元数据（metadata）是关于数据的信息。

<meta> 标签提供关于 HTML 文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。

典型的情况是，meta 元素被用于规定页面的描述、关键词、文档的作者、最后修改时间以及其他元数据。

<meta> 标签始终位于 head 元素中。

元数据可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。

### 针对搜索引擎的关键词

一些搜索引擎会利用 meta 元素的 name 和 content 属性来索引您的页面。

下面的 meta 元素定义页面的描述：

```
<meta name="description" content="Free Web tutorials on HTML, CSS, XML" />
```

下面的 meta 元素定义页面的关键词：

```
<meta name="keywords" content="HTML, CSS, XML" />
```

name 和 content 属性的作用是描述页面的内容。

## HTML <script> 元素

<script> 标签用于定义客户端脚本，比如 JavaScript。

我们会在稍后的章节讲解 script 元素。

## HTML 头部元素

| 标签                                       | 描述                   |
| ---------------------------------------- | -------------------- |
| [<head>](http://www.w3school.com.cn/tags/tag_head.asp) | 定义关于文档的信息。           |
| [<title>](http://www.w3school.com.cn/tags/tag_title.asp) | 定义文档标题。              |
| [<base>](http://www.w3school.com.cn/tags/tag_base.asp) | 定义页面上所有链接的默认地址或默认目标。 |
| [<link>](http://www.w3school.com.cn/tags/tag_link.asp) | 定义文档与外部资源之间的关系。      |
| [<meta>](http://www.w3school.com.cn/tags/tag_meta.asp) | 定义关于 HTML 文档的元数据。    |
| [<script>](http://www.w3school.com.cn/tags/tag_script.asp) | 定义客户端脚本。             |
| [<style>](http://www.w3school.com.cn/tags/tag_style.asp) | 定义文档的样式信息。           |