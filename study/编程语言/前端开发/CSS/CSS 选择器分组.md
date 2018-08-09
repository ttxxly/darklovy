## 选择器分组

假设希望 h2 元素和段落都有灰色。为达到这个目的，最容易的做法是使用以下声明：

```
h2, p {color:gray;}
```

将 h2 和 p 选择器放在规则左边，然后用逗号分隔，就定义了一个规则。其右边的样式（color:gray;）将应用到这两个选择器所引用的元素。逗号告诉浏览器，规则中包含两个不同的选择器。如果没有这个逗号，那么规则的含义将完全不同。参见后代选择器。

可以将任意多个选择器分组在一起，对此没有任何限制。

例如，如果您想把很多元素显示为灰色，可以使用类似如下的规则：

```
body, h2, p, table, th, td, pre, strong, em {color:gray;}
```

提示：通过分组，创作者可以将某些类型的样式“压缩”在一起，这样就可以得到更简洁的样式表。

以下的两组规则能得到同样的结果，不过可以很清楚地看出哪一个写起来更容易：

```
/* no grouping */
h1 {color:blue;}
h2 {color:blue;}
h3 {color:blue;}
h4 {color:blue;}
h5 {color:blue;}
h6 {color:blue;}

/* grouping */
h1, h2, h3, h4, h5, h6 {color:blue;}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping_selector)

分组提供了一些有意思的选择。例如，下例中的所有规则分组都是等价的，每个组只是展示了对选择器和声明分组的不同方法：

```
/* group 1 */
h1 {color:silver; background:white;}
h2 {color:silver; background:gray;}
h3 {color:white; background:gray;}
h4 {color:silver; background:white;}
b {color:gray; background:white;}

/* group 2 */
h1, h2, h4 {color:silver;}
h2, h3 {background:gray;}
h1, h4, b {background:white;}
h3 {color:white;}
b {color:gray;}

/* group 3 */
h1, h4 {color:silver; background:white;}
h2 {color:silver;}
h3 {color:white;}
h2, h3 {background:gray;}
b {color:gray; background:white;}

```

亲自试一试：

- [group 1](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping_selector_1)
- [group 2](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping_selector_2)
- [group 3](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping_selector_3)

请注意，group 3 中使用了“声明分组”。稍后我们会为您介绍“声明分组”。

## 通配符选择器

CSS2 引入了一种新的简单选择器 - 通配选择器（universal selector），显示为一个星号（*）。该选择器可以与任何元素匹配，就像是一个通配符。

例如，下面的规则可以使文档中的每个元素都为红色：

```
* {color:red;}
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping_selector_universal)

这个声明等价于列出了文档中所有元素的一个分组选择器。利用通配选择器，只需敲一次键（仅一个星号）就能使文档中所有元素的 color 属性值指定为 red。

## 声明分组

我们既可以对选择器进行分组，也可以对声明分组。

假设您希望所有 h1 元素都有红色背景，并使用 28 像素高的 Verdana 字体显示为蓝色文本，可以写以下样式：

```
h1 {font: 28px Verdana;}
h1 {color: blue;}
h1 {background: red;}

```

但是上面这种做法的效率并不高。尤其是当我们为一个有多个样式的元素创建这样一个列表时会很麻烦。相反，我们可以将声明分组在一起：

```
h1 {font: 28px Verdana; color: white; background: black;}
```

这与前面的 3 行样式表的效果完全相同。

注意，对声明分组，一定要在各个声明的最后使用分号，这很重要。浏览器会忽略样式表中的空白符。只要加了分号，就可以毫无顾忌地采用以下格式建立样式：

```
h1 {
  font: 28px Verdana;
  color: blue;
  background: red;
  }

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping_declaration)

怎么样，上面这种写法的可读性是不是更强。

不过，如果忽略了第二个分号，用户代理就会把这个样式表解释如下：

```
h1 {
  font: 28px Verdana;
  color: blue background: red;
  }

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping_declaration_error)

因为 background 对 color 来说不是一个合法值，而且由于只能为 color 指定一个关键字，所以用户代理会完全忽略这个 color 声明（包括 background: black 部分）。这样 h1 标题只会显示为蓝色，而没有红色背景，不过更有可能根本得不到蓝色的 h1。相反，这些标题只会显示为默认颜色（通常是黑色），而且根本没有背景色。font: 28px Verdana 声明仍能正常发挥作用，因为它确实正确地以一个分号结尾。

与选择器分组一样，声明分组也是一种便利的方法，可以缩短样式表，使之更清晰，也更易维护。

提示：在规则的最后一个声明后也加上分号是一个好习惯。在向规则增加另一个声明时，就不必担心忘记再插入一个分号。

## 结合选择器和声明的分组

我们可以在一个规则中结合选择器分组和声明分组，就可以使用很少的语句定义相对复杂的样式。

下面的规则为所有标题指定了一种复杂的样式：

```
h1, h2, h3, h4, h5, h6 {
  color:gray;
  background: white;
  padding: 10px;
  border: 1px solid black;
  font-family: Verdana;
  }

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_grouping)

上面这条规则将所有标题的样式定义为带有白色背景的灰色文本，其内边距是 10 像素，并带有 1 像素的实心边框，文本字体是 Verdana。

- 