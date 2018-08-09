几乎所有浏览器都支持 `<div>` 标签。

`<div>` 标签可定义文档中的分区或节(division/section)，将文档分割成独立的、不同的部分。

`<div>` 是一个块级元素。这意味着它的内容自动开始一个新行。实际上，换行是 <div> 固有的唯一格式表现。

可以通过 `<div>` 的 class 或 id 应用额外的样式。

#### HTML 与 XHTML 之间的差异

```
在 HTML 4.01 中，div 元素的 "align" 属性不被赞成使用。
在 XHTML 1.0 Strict DTD 中，div 元素的 "align" 属性不被支持。
```

#### 可选属性

| 属性                                                       | 值                           | 描述                                                         |
| ---------------------------------------------------------- | ---------------------------- | ------------------------------------------------------------ |
| [align](http://www.w3school.com.cn/tags/att_div_align.asp) | left\|right\|center\|justify | 不赞成使用。请使用样式取而代之。规定 div 元素中的内容的对齐方式。 |

#### 案例分析

```
<body>

 <h1>NEWS WEBSITE</h1>
  <p>some text. some text. some text...</p>
  ...

 <div class="news">
  <h2>News headline 1</h2>
  <p>some text. some text. some text...</p>
  ...
 </div>

 <div class="news">
  <h2>News headline 2</h2>
  <p>some text. some text. some text...</p>
  ...
 </div>

 ...
</body>

```

**`div`标签同样支持HTML的全局属性和事件属性**。

[戳我查看HTML的全局属性](https://blog.csdn.net/jdliyao/article/details/80011899)

[戳我查看HTML的事件属性](https://blog.csdn.net/jdliyao/article/details/80012046)

发表于：

```
https://blog.csdn.net/jdliyao/article/details/80012107
```

