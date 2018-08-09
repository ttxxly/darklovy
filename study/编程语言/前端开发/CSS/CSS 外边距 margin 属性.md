**围绕在元素边框的空白区域是外边距。设置外边距会在元素外创建额外的“空白”。**

**设置外边距的最简单的方法就是使用 margin 属性，这个属性接受任何长度单位、百分数值甚至负值。**

## CSS margin 属性

设置外边距的最简单的方法就是使用 [margin 属性](http://www.w3school.com.cn/cssref/pr_margin.asp)。

margin 属性接受任何长度单位，可以是像素、英寸、毫米或 em。

margin 可以设置为 auto。更常见的做法是为外边距设置长度值。下面的声明在 h1 元素的各个边上设置了 1/4 英寸宽的空白：

```
h1 {margin : 0.25in;}
```

下面的例子为 h1 元素的四个边分别定义了不同的外边距，所使用的长度单位是像素 (px)：

```
h1 {margin : 10px 0px 15px 5px;}
```

与内边距的设置相同，这些值的顺序是从上外边距 (top) 开始围着元素顺时针旋转的：

```
margin: top right bottom left
```

另外，还可以为 margin 设置一个百分比数值：

```
p {margin : 10%;}
```

百分数是相对于父元素的 width 计算的。上面这个例子为 p 元素设置的外边距是其父元素的 width 的 10%。

margin 的默认值是 0，所以如果没有为 margin 声明一个值，就不会出现外边距。但是，在实际中，浏览器对许多元素已经提供了预定的样式，外边距也不例外。例如，在支持 CSS 的浏览器中，外边距会在每个段落元素的上面和下面生成“空行”。因此，如果没有为 p 元素声明外边距，浏览器可能会自己应用一个外边距。当然，只要你特别作了声明，就会覆盖默认样式。

## 值复制

还记得吗？我们曾经在前两节中提到过值复制。下面我们为您讲解如何使用值复制。

有时，我们会输入一些重复的值：

```
p {margin: 0.5em 1em 0.5em 1em;}
```

通过值复制，您可以不必重复地键入这对数字。上面的规则与下面的规则是等价的：

```
p {margin: 0.5em 1em;}
```

这两个值可以取代前面 4 个值。这是如何做到的呢？CSS 定义了一些规则，允许为外边距指定少于 4 个值。规则如下：

- 如果缺少左外边距的值，则使用右外边距的值。
- 如果缺少下外边距的值，则使用上外边距的值。
- 如果缺少右外边距的值，则使用上外边距的值。

下图提供了更直观的方法来了解这一点：

换句话说，如果为外边距指定了 3 个值，则第 4 个值（即左外边距）会从第 2 个值（右外边距）复制得到。如果给定了两个值，第 4 个值会从第 2 个值复制得到，第 3 个值（下外边距）会从第 1 个值（上外边距）复制得到。最后一个情况，如果只给定一个值，那么其他 3 个外边距都由这个值（上外边距）复制得到。

利用这个简单的机制，您只需指定必要的值，而不必全部都应用 4 个值，例如：

```
h1 {margin: 0.25em 1em 0.5em;}	/* 等价于 0.25em 1em 0.5em 1em */
h2 {margin: 0.5em 1em;}		/* 等价于 0.5em 1em 0.5em 1em */
p {margin: 1px;}			/* 等价于 1px 1px 1px 1px */

```

这种办法有一个小缺点，您最后肯定会遇到这个问题。假设希望把 p 元素的上外边距和左外边距设置为 20 像素，下外边距和右外边距设置为 30 像素。在这种情况下，必须写作：

```
p {margin: 20px 30px 30px 20px;}
```

这样才能得到您想要的结果。遗憾的是，在这种情况下，所需值的个数没有办法更少了。

再来看另外一个例子。如果希望除了左外边距以外所有其他外边距都是 auto（左外边距是 20px）：

```
p {margin: auto auto auto 20px;}
```

同样的，这样才能得到你想要的效果。问题在于，键入这些 auto 有些麻烦。如果您只是希望控制元素单边上的外边距，请使用单边外边距属性。

## 单边外边距属性

您可以使用单边外边距属性为元素单边上的外边距设置值。假设您希望把 p 元素的左外边距设置为 20px。不必使用 margin（需要键入很多 auto），而是可以采用以下方法：

```
p {margin-left: 20px;}
```

您可以使用下列任何一个属性来只设置相应上的外边距，而不会直接影响所有其他外边距：

- [margin-top](http://www.w3school.com.cn/cssref/pr_margin-top.asp)
- [margin-right](http://www.w3school.com.cn/cssref/pr_margin-right.asp)
- [margin-bottom](http://www.w3school.com.cn/cssref/pr_margin-bottom.asp)
- [margin-left](http://www.w3school.com.cn/cssref/pr_margin-left.asp)

一个规则中可以使用多个这种单边属性，例如：

```
h2 {
  margin-top: 20px;
  margin-right: 30px;
  margin-bottom: 30px;
  margin-left: 20px;
  }

```

当然，对于这种情况，使用 margin 可能更容易一些：

```
p {margin: 20px 30px 30px 20px;}
```

不论使用单边属性还是使用 margin，得到的结果都一样。一般来说，如果希望为多个边设置外边距，使用 margin 会更容易一些。不过，从文档显示的角度看，实际上使用哪种方法都不重要，所以应该选择对自己来说更容易的一种方法。

## 提示和注释

提示：Netscape 和 IE 对 body 标签定义的默认边距（margin）值是 8px。而 Opera 不是这样。相反地，Opera 将内部填充（padding）的默认值定义为 8px，因此如果希望对整个网站的边缘部分进行调整，并将之正确显示于 Opera 中，那么必须对 body 的 padding 进行自定义。

## CSS 外边距实例：

- [设置文本的左外边距](http://www.w3school.com.cn/tiy/t.asp?f=csse_margin-left)

  本例演示如何设置文本的左外边距。

- [设置文本的右外边距](http://www.w3school.com.cn/tiy/t.asp?f=csse_margin-right)

  本例演示如何设置文本的右外边距。

- [设置文本的上外边距](http://www.w3school.com.cn/tiy/t.asp?f=csse_margin-top)

  本例演示如何设置文本的上外边距。

- [设置文本的下外边距](http://www.w3school.com.cn/tiy/t.asp?f=csse_margin-bottom)

  本例演示如何设置文本的下外边距。

- [所有的外边距属性在一个声明中。](http://www.w3school.com.cn/tiy/t.asp?f=csse_margin)

  本例演示如何将所有的外边距属性设置于一个声明中。

## CSS 外边距属性

| 属性                                                         | 描述                                       |
| ------------------------------------------------------------ | ------------------------------------------ |
| [margin](http://www.w3school.com.cn/cssref/pr_margin.asp)    | 简写属性。在一个声明中设置所有外边距属性。 |
| [margin-bottom](http://www.w3school.com.cn/cssref/pr_margin-bottom.asp) | 设置元素的下外边距。                       |
| [margin-left](http://www.w3school.com.cn/cssref/pr_margin-left.asp) | 设置元素的左外边距。                       |
| [margin-right](http://www.w3school.com.cn/cssref/pr_margin-right.asp) | 设置元素的右外边距。                       |
| [margin-top](http://www.w3school.com.cn/cssref/pr_margin-top.asp) | 设置元素的上外边距。                       |