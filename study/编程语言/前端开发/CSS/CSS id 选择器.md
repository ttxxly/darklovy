## id 选择器

**id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式。**

**id 选择器以 "#" 来定义。**

下面的两个 id 选择器，第一个可以定义元素的颜色为红色，第二个定义元素的颜色为绿色：

```
#red {color:red;}
#green {color:green;}

```

下面的 HTML 代码中，id 属性为 red 的 p 元素显示为红色，而 id 属性为 green 的 p 元素显示为绿色。

```
<p id="red">这个段落是红色。</p>
<p id="green">这个段落是绿色。</p>

```

注意：id 属性只能在每个 HTML 文档中出现一次。想知道原因吗，请参阅 [XHTML:网站重构](http://www.w3school.com.cn/xhtml/xhtml_structural_01.asp)。

## id 选择器和派生选择器

**在现代布局中，id 选择器常常用于建立派生选择器。**

```
#sidebar p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}

```

上面的样式只会应用于出现在 id 是 sidebar 的元素内的段落。这个元素很可能是 div 或者是表格单元，尽管它也可能是一个表格或者其他块级元素。它甚至可以是一个内联元素，比如 <em></em> 或者 <span></span>，不过这样的用法是非法的，因为不可以在内联元素 <span> 中嵌入 <p> （如果你忘记了原因，请参阅 [XHTML:网站重构](http://www.w3school.com.cn/xhtml/xhtml_structural_01.asp)）。

### 一个选择器，多种用法

**即使被标注为 sidebar 的元素只能在文档中出现一次，这个 id 选择器作为派生选择器也可以被使用很多次：**

```
#sidebar p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}

#sidebar h2 {
	font-size: 1em;
	font-weight: normal;
	font-style: italic;
	margin: 0;
	line-height: 1.5;
	text-align: right;
	}

```

在这里，与页面中的其他 p 元素明显不同的是，sidebar 内的 p 元素得到了特殊的处理，同时，与页面中其他所有 h2 元素明显不同的是，sidebar 中的 h2 元素也得到了不同的特殊处理。

## 单独的选择器

**id 选择器即使不被用来创建派生选择器，它也可以独立发挥作用：**

```
#sidebar {
	border: 1px dotted #000;
	padding: 10px;
	}
```

根据这条规则，id 为 sidebar 的元素将拥有一个像素宽的黑色点状边框，同时其周围会有 10 个像素宽的内边距（padding，内部空白）。老版本的 Windows/IE 浏览器可能会忽略这条规则，除非你特别地定义这个选择器所属的元素：

```
div#sidebar {
	border: 1px dotted #000;
	padding: 10px;
	}
```

## 相关内容

如果您需要更深入地学习关于 ID 选择器的知识，请阅读 W3School 的高级教程：[CSS ID 选择器详解](http://www.w3school.com.cn/css/css_selector_id.asp)。