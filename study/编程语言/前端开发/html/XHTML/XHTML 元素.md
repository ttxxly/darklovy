**XHTML 元素是以 XML 格式编写的 HTML 元素。**

## XHTML 元素 - 语法规则

- XHTML 元素必须*正确嵌套*
- XHTML 元素必须始终*关闭*
- XHTML 元素必须*小写*
- XHTML 文档必须有*一个根元素*

## XHTML 元素必须正确嵌套

在 HTML 中，某些元素可以不正确地彼此嵌套在一起，就像这样：

```
<b><i>This text is bold and italic</b></i>
```

在 XHTML 中，所有元素必须正确地彼此嵌套，就像这样：

```
<b><i>This text is bold and italic</i></b>
```

## XHTML 元素必须始终关闭

这是错误的：

```
<p>This is a paragraph
<p>This is another paragraph

```

这是正确的：

```
<p>This is a paragraph</p>
<p>This is another paragraph</p>

```

## 空元素也必须关闭

这是错误的：

```
A break: <br>
A horizontal rule: <hr>
An image: <img src="happy.gif" alt="Happy face">

```

这是正确的：

```
A break: <br />
A horizontal rule: <hr />
An image: <img src="happy.gif" alt="Happy face" />

```

## XHTML 元素必须小写

这是错误的：

```
<BODY>
<P>This is a paragraph</P>
</BODY>

```

这是正确的：

```
<body>
<p>This is a paragraph</p>
</body>
```