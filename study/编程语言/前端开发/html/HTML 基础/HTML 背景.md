**好的背景使站点看上去特别棒。**

## 实例

- [搭配良好的背景和颜色](http://www.w3school.com.cn/tiy/t.asp?f=html_back_good)

  一个背景颜色和文字颜色搭配良好的例子，使页面中的文字易于阅读。

- [搭配得不好的背景和颜色](http://www.w3school.com.cn/tiy/t.asp?f=html_back_bad)

  一个背景颜色和文字颜色搭配得不好的例子，使页面中的文字难于阅读。

（[可以在本页底端找到更多实例](http://www.w3school.com.cn/html/html_backgrounds.asp#more_examples)。）

## 背景（Backgrounds）

<body> 拥有两个配置背景的标签。背景可以是颜色或者图像。

### 背景颜色（Bgcolor）

背景颜色属性将背景设置为某种颜色。属性值可以是十六进制数、RGB 值或颜色名。

```
<body bgcolor="#000000">
<body bgcolor="rgb(0,0,0)">
<body bgcolor="black">
```

以上的代码均将背景颜色设置为黑色。

### 背景（Background）

背景属性将背景设置为图像。属性值为图像的URL。如果图像尺寸小于浏览器窗口，那么图像将在整个浏览器窗口进行复制。

```
<body background="clouds.gif">
<body background="http://www.w3school.com.cn/clouds.gif">
```

URL可以是相对地址，如第一行代码。也可以使绝对地址，如第二行代码。

提示：如果你打算使用背景图片，你需要紧记一下几点：

- 背景图像是否增加了页面的加载时间。小贴士：图像文件不应超过 10k。
- 背景图像是否与页面中的其他图象搭配良好。
- 背景图像是否与页面中的文字颜色搭配良好。
- 图像在页面中平铺后，看上去还可以吗？
- 对文字的注意力被背景图像喧宾夺主了吗？

## 基本的注意事项 - 有用的提示：

<body> 标签中的背景颜色（bgcolor）、背景（background）和文本（text）属性在最新的 HTML 标准（HTML4 和 XHTML）中已被废弃。W3C 在他们的推荐标准中已删除这些属性。

应该使用层叠样式表（CSS）来定义 HTML 元素的布局和显示属性。

## [更多实例]()

- [可用性强的背景图像](http://www.w3school.com.cn/tiy/t.asp?f=html_back_img)

  背景图像和文字颜色使页面文本易于阅读的例子。

- [可用性强的背景图像 2](http://www.w3school.com.cn/tiy/t.asp?f=html_back_img2)

  另一个背景图像和文字颜色使页面文本易于阅读的例子。

- [可用性差的背景图像](http://www.w3school.com.cn/tiy/t.asp?f=html_back_imgbad)

  背景图像和文字颜色使页面文本不易阅读的例子。


- 