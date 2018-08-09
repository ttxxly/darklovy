## 演示：导航栏

- [HOME](http://www.w3school.com.cn/css/css_navbar.asp#)
- [NEWS](http://www.w3school.com.cn/css/css_navbar.asp#)
- [ARTICLES](http://www.w3school.com.cn/css/css_navbar.asp#)
- [FORUM](http://www.w3school.com.cn/css/css_navbar.asp#)
- [CONTACT](http://www.w3school.com.cn/css/css_navbar.asp#)
- [ABOUT](http://www.w3school.com.cn/css/css_navbar.asp#)

## 导航栏

拥有易用的导航条对于任何网站都很重要。

通过 CSS，您能够把乏味的 HTML 菜单转换为漂亮的导航栏。

## 导航栏 = 链接列表

导航栏需要标准的 HTML 作为基础。

在我们的例子中，将用标准的 HTML 列表来构建导航栏。

导航栏基本上是一个链接列表，因此使用 <ul> 和 <li> 元素是非常合适的：

#### 实例

```
<ul>
<li><a href="default.asp">Home</a></li>
<li><a href="news.asp">News</a></li>
<li><a href="contact.asp">Contact</a></li>
<li><a href="about.asp">About</a></li>
</ul>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_basic_html)

现在，让我们从列表中去掉圆点和外边距：

#### 实例

```
ul
{
list-style-type:none;
margin:0;
padding:0;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_basic_css)

### 例子解释：

- list-style-type:none - 删除圆点。导航栏不需要列表项标记。
- 把外边距和内边距设置为 0 可以去除浏览器的默认设定。

以上例子中的代码是用在垂直、水平导航栏中的标准代码。

## 垂直导航栏

如需构建垂直导航栏，我们只需要定义 <a> 元素的样式，除了上面的代码之外：

### 实例

```
a
{
display:block;
width:60px;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_vertical)

### 例子解释：

- display:block - 把链接显示为块元素可使整个链接区域可点击（不仅仅是文本），同时也允许我们规定宽度。
- width:60px - 块元素默认占用全部可用宽度。我们需要规定 60 像素的宽度。

提示：请同时看一看我们[完整样式的导航栏实例](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_vertical_advanced)。

注释：请始终规定垂直导航栏中 <a> 元素的宽度。如果省略宽度，IE6 会产生意想不到的结果。

## 水平导航栏

有两种创建水平导航栏的方法。使用行内或浮动列表项。

两种方法都不错，但是如果您希望链接拥有相同的尺寸，就必须使用浮动方法。

### 行内列表项

除了上面的“标准”代码，构建水平导航栏的方法之一是将 <li> 元素规定为行内元素：

#### 实例

```
li
{
display:inline;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_horizontal)

#### 例子解释：

display:inline; - 默认地，<li> 元素是块元素。在这里，我们去除了每个列表项前后的换行，以便让它们在一行中显示。

提示：请看一下我们[完整样式的水平导航栏实例](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_horizontal_advanced)。

### 对列表项进行浮动

在上面的例子中，链接的宽度是不同的。

为了让所有链接拥有相等的宽度，浮动 <li> 元素并规定 <a> 元素的宽度：

#### 实例

```
li
{
float:left;
}
a
{
display:block;
width:60px;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_horizontal_float)

#### 例子解释：

- float:left - 使用 float 来把块元素滑向彼此。
- display:block - 把链接显示为块元素可使整个链接区域可点击（不仅仅是文本），同时也允许我们规定宽度。
- width:60px - 由于块元素默认占用全部可用宽度，链接无法滑动至彼此相邻。我们需要规定 60 像素的宽度。

提示：请看一下我们[完整样式的水平导航栏实例](http://www.w3school.com.cn/tiy/t.asp?f=css_navbar_horizontal_float_advanced)。