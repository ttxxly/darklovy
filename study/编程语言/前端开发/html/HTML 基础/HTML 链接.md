HTML 链接是通过 <a> 标签来进行定义的。

```
<a href="http://www.w3school.com.cn">This is a link</a>
```

**HTML 使用超级链接与网络上的另一个文档相连。**

**几乎可以在所有的网页中找到链接。点击链接可以从一张页面跳转到另一张页面。**

## 实例

- [创建超级链接](http://www.w3school.com.cn/tiy/t.asp?f=html_links)

  本例演示如何在 HTML 文档中创建链接。

- [将图像作为链接](http://www.w3school.com.cn/tiy/t.asp?f=html_imglink)

  本例演示如何使用图像作为链接。

（[可以在本页底端找到更多实例](http://www.w3school.com.cn/html/html_links.asp#more_examples)）

## HTML 超链接（链接）

超链接可以是一个字，一个词，或者一组词，也可以是一幅图像，您可以点击这些内容来跳转到新的文档或者当前文档中的某个部分。

当您把鼠标指针移动到网页中的某个链接上时，箭头会变为一只小手。

我们通过使用 <a> 标签在 HTML 中创建链接。

有两种使用 <a> 标签的方式：

1. 通过使用 href 属性 - 创建指向另一个文档的链接
2. 通过使用 name 属性 - 创建文档内的书签

延伸阅读：[什么是超文本？](http://www.w3school.com.cn/tags/tag_term_hypertext.asp)

## HTML 链接语法

链接的 HTML 代码很简单。它类似这样：

```
<a href="url">Link text</a>
```

href 属性规定链接的目标。

开始标签和结束标签之间的文字被作为超级链接来显示。

### 实例

```
<a href="http://www.w3school.com.cn/">Visit W3School</a>
```

上面这行代码显示为：[Visit W3School](http://www.w3school.com.cn/)

点击这个超链接会把用户带到 W3School 的首页。

提示："链接文本" 不必一定是文本。图片或其他 HTML 元素都可以成为链接。

## HTML 链接 - target 属性

使用 Target 属性，你可以定义被链接的文档在何处显示。

下面的这行会在新窗口打开文档：

```
<a href="http://www.w3school.com.cn/" target="_blank">Visit W3School!</a>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_link_target)

## HTML 链接 - name 属性

name 属性规定锚（anchor）的名称。

您可以使用 name 属性创建 HTML 页面中的书签。

书签不会以任何特殊方式显示，它对读者是不可见的。

当使用命名锚（named anchors）时，我们可以创建直接跳至该命名锚（比如页面中某个小节）的链接，这样使用者就无需不停地滚动页面来寻找他们需要的信息了。

### 命名锚的语法：

```
<a name="label">锚（显示在页面上的文本）</a>
```

提示：锚的名称可以是任何你喜欢的名字。

提示：您可以使用 id 属性来替代 name 属性，命名锚同样有效。

### 实例

首先，我们在 HTML 文档中对锚进行命名（创建一个书签）：

```
<a name="tips">基本的注意事项 - 有用的提示</a>
```

然后，我们在同一个文档中创建指向该锚的链接：

```
<a href="#tips">有用的提示</a>
```

您也可以在其他页面中创建指向该锚的链接：

```
<a href="http://www.w3school.com.cn/html/html_links.asp#tips">有用的提示</a>
```

在上面的代码中，我们将 # 符号和锚名称添加到 URL 的末端，就可以直接链接到 tips 这个命名锚了。

具体效果：[有用的提示](http://www.w3school.com.cn/html/html_links.asp#tips)

## [基本的注意事项 - 有用的提示：]()

注释：请始终将正斜杠添加到子文件夹。假如这样书写链接：href="http://www.w3school.com.cn/html"，就会向服务器产生两次 HTTP 请求。这是因为服务器会添加正斜杠到这个地址，然后创建一个新的请求，就像这样：href="http://www.w3school.com.cn/html/"。

提示：命名锚经常用于在大型文档开始位置上创建目录。可以为每个章节赋予一个命名锚，然后把链接到这些锚的链接放到文档的上部。如果您经常访问百度百科，您会发现其中几乎每个词条都采用这样的导航方式。

提示：假如浏览器找不到已定义的命名锚，那么就会定位到文档的顶端。不会有错误发生。

## [更多实例]()

- [在新的浏览器窗口打开链接](http://www.w3school.com.cn/tiy/t.asp?f=html_link_target)

  本例演示如何在新窗口打开一个页面，这样的话访问者就无需离开你的站点了。

- [链接到同一个页面的不同位置](http://www.w3school.com.cn/tiy/t.asp?f=html_link_locations)

  本例演示如何使用链接跳转至文档的另一个部分

- [跳出框架](http://www.w3school.com.cn/tiy/t.asp?f=html_frame_getfree)

  本例演示如何跳出框架，假如你的页面被固定在框架之内。

- [创建电子邮件链接](http://www.w3school.com.cn/tiy/t.asp?f=html_mailto)

  本例演示如何链接到一个邮件。（本例在安装邮件客户端程序后才能工作。）

- [创建电子邮件链接 2](http://www.w3school.com.cn/tiy/t.asp?f=html_mailto2)

  本例演示更加复杂的邮件链接。

## HTML 链接标签

| 标签                                       | 描述   |
| ---------------------------------------- | ---- |
| [](http://www.w3school.com.cn/tags/tag_a.asp) | 定义锚。 |