**类选择器允许以一种独立于文档元素的方式来指定样式。**

## CSS 类选择器

类选择器允许以一种独立于文档元素的方式来指定样式。

该选择器可以单独使用，也可以与其他元素结合使用。

提示：只有适当地标记文档后，才能使用这些选择器，所以使用这两种选择器通常需要先做一些构想和计划。

要应用样式而不考虑具体设计的元素，最常用的方法就是使用类选择器。

### 修改 HTML 代码

在使用类选择器之前，需要修改具体的文档标记，以便类选择器正常工作。

为了将类选择器的样式与元素关联，必须将 class 指定为一个适当的值。请看下面的 HTML 代码：

```
<h1 class="important">
This heading is very important.
</h1>

<p class="important">
This paragraph is very important.
</p>

```

在上面的代码中，两个元素的 class 都指定为 important：第一个标题（ h1 元素），第二个段落（p 元素）。

### 语法

然后我们使用以下语法向这些归类的元素应用样式，即类名前有一个点号（.），然后结合通配选择器：

```
*.important {color:red;}
```

如果您只想选择所有类名相同的元素，可以在类选择器中忽略通配选择器，这没有任何不好的影响：

```
.important {color:red;}
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_class_1)

### 结合元素选择器

类选择器可以结合元素选择器来使用。

例如，您可能希望只有段落显示为红色文本：

```
p.important {color:red;}
```

选择器现在会匹配 class 属性包含 important 的所有 p 元素，但是其他任何类型的元素都不匹配，不论是否有此 class 属性。选择器 p.important 解释为：“其 class 属性值为 important 的所有段落”。 因为 h1 元素不是段落，这个规则的选择器与之不匹配，因此 h1 元素不会变成红色文本。

如果你确实希望为 h1 元素指定不同的样式，可以使用选择器 h1.important：

```
p.important {color:red;}
h1.important {color:blue;}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_class_2)

## CSS 多类选择器

在上一节中，我们处理了 class 值中包含一个词的情况。在 HTML 中，一个 class 值中可能包含一个词列表，各个词之间用空格分隔。例如，如果希望将一个特定的元素同时标记为重要（important）和警告（warning），就可以写作：

```
<p class="important warning">
This paragraph is a very important warning.
</p>

```

这两个词的顺序无关紧要，写成 warning important 也可以。

我们假设 class 为 important 的所有元素都是粗体，而 class 为 warning 的所有元素为斜体，class 中同时包含 important 和 warning 的所有元素还有一个银色的背景 。就可以写作：

```
.important {font-weight:bold;}
.warning {font-style:italic;}
.important.warning {background:silver;}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_class_multiple)

通过把两个类选择器链接在一起，仅可以选择*同时包含这些类名*的元素（类名的顺序不限）。

如果一个多类选择器包含类名列表中没有的一个类名，匹配就会失败。请看下面的规则：

```
.important.urgent {background:silver;}
```

不出所料，这个选择器将只匹配 class 属性中包含词 important 和 urgent 的 p 元素。因此，如果一个 p 元素的 class 属性中只有词 important 和 warning，将不能匹配。不过，它能匹配以下元素：

```
<p class="important urgent warning">
This paragraph is a very important and urgent warning.
</p>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_class_multiple_2)

重要事项：在 IE7 之前的版本中，不同平台的 Internet Explorer 都不能正确地处理多类选择器。

- 