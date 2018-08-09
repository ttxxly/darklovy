在 CSS 中，可以使用多种属性来水平对齐元素。

## 对齐块元素

块元素指的是占据全部可用宽度的元素，并且在其前后都会换行。

块元素的例子：

```
<h1>
<p>
<div>

```

对于文本对齐，请参见 [CSS 文本](http://www.w3school.com.cn/css/css_text.asp)一章。

在本教程中，我们将向您展示出于布局目的如何水平对齐块级元素。

## 使用 margin 属性来水平对齐

可通过将左和右外边距设置为 "auto"，来对齐块元素。

注释：除非已经声明了 !DOCTYPE，否则使用 margin:auto 在 IE8 以及更早的版本中是无效的。

把左和右外边距设置为 auto，规定的是均等地分配可用的外边距。结果就是居中的元素：

### 实例

```
.center
{
margin-left:auto;
margin-right:auto;
width:70%;
background-color:#b0e0e6;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_align_margin)

提示：如果宽度是 100%，则对齐没有效果。

注释：在 IE5 中，对于块元素存在一个外边距处理方面的 BUG。如需使上面的例子在 IE5 中有效，请添加一些额外的代码。[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_align_margin_ie5)。

## 使用 position 属性进行左和右对齐

对齐元素的方法之一是使用绝对定位：

### 实例

```
.right
{
position:absolute;
right:0px;
width:300px;
background-color:#b0e0e6;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_align_position)

注释：绝对定位元素会被从正常流中删除，并且能够交叠元素。

## 跨浏览器兼容性问题

当像这样对齐元素时，对 <body> 元素的外边距和内边距进行预定义是一个好主意。这样可以避免在不同的浏览器中出现可见的差异。

当使用 position 属性时，IE8 以及更早的版本存在一个问题。如果容器元素（在我们的案例中是 <div class="container">）设置了指定的宽度，并且省略了 !DOCTYPE 声明，那么 IE8 以及更早的版本会在右侧增加 17px 的外边距。这似乎是为滚动条预留的空间。当使用 position 属性时，请始终设置 !DOCTYPE 声明：

### 实例

```
body
{
margin:0;
padding:0;
}
.container
{
position:relative;
width:100%;
}
.right
{
position:absolute;
right:0px;
width:300px;
background-color:#b0e0e6;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_align_position_crossbrowser)

## 使用 float 属性来进行左和右对齐

对齐元素的另一种方法是使用 float 属性：

### 实例

```
.right
{
float:right;
width:300px;
background-color:#b0e0e6;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_align_float)

## 跨浏览器兼容性问题

当像这样对齐元素时，对 <body> 元素的外边距和内边距进行预定义是一个好主意。这样可以避免在不同的浏览器中出现可见的差异。

当使用 float 属性时，IE8 以及更早的版本存在一个问题。如果省略 !DOCTYPE 声明，那么 IE8 以及更早的版本会在右侧增加 17px 的外边距。这似乎是为滚动条预留的空间。当使用 float 属性时，请始终设置 !DOCTYPE 声明：

### 实例

```
body
{
margin:0;
padding:0;
}

.right
{
float:right;
width:300px;
background-color:#b0e0e6;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=css_align_float_crossbrowser)