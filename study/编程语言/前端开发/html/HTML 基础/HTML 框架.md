**通过使用框架，你可以在同一个浏览器窗口中显示不止一个页面。**

## 实例

- [垂直框架](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_cols)

  本例演示：如何使用三份不同的文档制作一个垂直框架。

- [水平框架](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_rows)

  本例演示：如何使用三份不同的文档制作一个水平框架。

（[可以在本页底端找到更多实例](http://www.w3school.com.cn/html/html_frames.asp#more_examples)。）

## 框架

通过使用框架，你可以在同一个浏览器窗口中显示不止一个页面。每份HTML文档称为一个框架，并且每个框架都独立于其他的框架。

使用框架的坏处：

- 开发人员必须同时跟踪更多的HTML文档
- 很难打印整张页面


- 框架结构标签（<frameset>）

  框架结构标签（<frameset>）定义如何将窗口分割为框架每个 frameset 定义了一系列行*或*列rows/columns 的值规定了每行或每列占据屏幕的面积

编者注：frameset 标签也被某些文章和书籍译为框架集。

## 框架标签（Frame）

Frame 标签定义了放置在每个框架中的 HTML 文档。

在下面的这个例子中，我们设置了一个两列的框架集。第一列被设置为占据浏览器窗口的 25%。第二列被设置为占据浏览器窗口的 75%。HTML 文档 "frame_a.htm" 被置于第一个列中，而 HTML 文档 "frame_b.htm" 被置于第二个列中：

```
<frameset cols="25%,75%">
   <frame src="frame_a.htm">
   <frame src="frame_b.htm">
</frameset>

```

## 基本的注意事项 - 有用的提示：

假如一个框架有可见边框，用户可以拖动边框来改变它的大小。为了避免这种情况发生，可以在 <frame> 标签中加入：noresize="noresize"。

为不支持框架的浏览器添加 <noframes> 标签。

重要提示：不能将 <body></body> 标签与 <frameset></frameset> 标签同时使用！不过，假如你添加包含一段文本的 <noframes> 标签，就必须将这段文字嵌套于 <body></body> 标签内。（在下面的第一个实例中，可以查看它是如何实现的。）

## [更多实例]()

- [如何使用  标签](http://www.w3school.com.cn/tiy/t.asp?f=html_noframes)

  本例演示：如何使用 <noframes> 标签。

- [混合框架结构](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_mix)

  本例演示如何制作含有三份文档的框架结构，同时将他们混合置于行和列之中。

- [含有 noresize="noresize" 属性的框架结构](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_noresize)

  本例演示 noresize 属性。在本例中，框架是不可调整尺寸的。在框架间的边框上拖动鼠标，你会发现边框是无法移动的。

- [导航框架](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_navigation)

  本例演示如何制作导航框架。导航框架包含一个将第二个框架作为目标的链接列表。名为 "contents.htm" 的文件包含三个链接。

- [内联框架](http://www.w3school.com.cn/tiy/t.asp?f=html_iframe)

  本例演示如何创建内联框架（HTML 页中的框架）。

- [跳转至框架内的一个指定的节](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_jump)

  本例演示两个框架。其中的一个框架设置了指向另一个文件内指定的节的链接。这个"link.htm"文件内指定的节使用 <a name="C10"> 进行标识。

- [使用框架导航跳转至指定的节](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_navigation2)

  本例演示两个框架。左侧的导航框架包含了一个链接列表，这些链接将第二个框架作为目标。第二个框架显示被链接的文档。导航框架其中的链接指向目标文件中指定的节。