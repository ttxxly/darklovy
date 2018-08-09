**你可以使用 HTML 创建表格。**

## 实例

- [表格](http://www.w3school.com.cn/tiy/t.asp?f=html_tables)

  这个例子演示如何在 HTML 文档中创建表格。

- [表格边框](http://www.w3school.com.cn/tiy/t.asp?f=html_table_borders)

  本例演示各种类型的表格边框。

（[可以在本页底端找到更多实例](http://www.w3school.com.cn/html/html_tables.asp#more_examples)。）

## 表格

表格由 <table> 标签来定义。每个表格均有若干行（由 <tr> 标签定义），每行被分割为若干单元格（由 <td> 标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

```
<table border="1">
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>
```

在浏览器显示如下：

| row 1, cell 1 | row 1, cell 2 |
| ------------- | ------------- |
| row 2, cell 1 | row 2, cell 2 |

## 表格和边框属性

如果不定义边框属性，表格将不显示边框。有时这很有用，但是大多数时候，我们希望显示边框。

使用边框属性来显示一个带有边框的表格：

```
<table border="1">
<tr>
<td>Row 1, cell 1</td>
<td>Row 1, cell 2</td>
</tr>
</table>
```

## 表格的表头

表格的表头使用 <th> 标签进行定义。

大多数浏览器会把表头显示为粗体居中的文本：

```
<table border="1">
<tr>
<th>Heading</th>
<th>Another Heading</th>
</tr>
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>
```

在浏览器显示如下：

| Heading       | Another Heading |
| ------------- | --------------- |
| row 1, cell 1 | row 1, cell 2   |
| row 2, cell 1 | row 2, cell 2   |

## 表格中的空单元格

在一些浏览器中，没有内容的表格单元显示得不太好。如果某个单元格是空的（没有内容），浏览器可能无法显示出这个单元格的边框。

```
<table border="1">
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td></td>
<td>row 2, cell 2</td>
</tr>
</table>
```

浏览器可能会这样显示：

注意：这个空的单元格的边框没有被显示出来。为了避免这种情况，在空单元格中添加一个空格占位符，就可以将边框显示出来。

```
<table border="1">
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>row 2, cell 2</td>
</tr>
</table>
```

在浏览器中显示如下：

| row 1, cell 1 | row 1, cell 2 |
| ------------- | ------------- |
|               | row 2, cell 2 |

## [更多实例]()

- [没有边框的表格](http://www.w3school.com.cn/tiy/t.asp?f=html_tables2)

  本例演示一个没有边框的表格。

- [表格中的表头(Heading)](http://www.w3school.com.cn/tiy/t.asp?f=html_table_headers)

  本例演示如何显示表格表头。

- [空单元格](http://www.w3school.com.cn/tiy/t.asp?f=html_table_nbsp)

  本例展示如何使用 "&nbsp;" 处理没有内容的单元格。

- [带有标题的表格](http://www.w3school.com.cn/tiy/t.asp?f=html_tables3)

  本例演示一个带标题 (caption) 的表格

- [跨行或跨列的表格单元格](http://www.w3school.com.cn/tiy/t.asp?f=html_table_span)

  本例演示如何定义跨行或跨列的表格单元格。

- [表格内的标签](http://www.w3school.com.cn/tiy/t.asp?f=html_table_elements)

  本例演示如何显示在不同的元素内显示元素。

- [单元格边距(Cell padding)](http://www.w3school.com.cn/tiy/t.asp?f=html_table_cellpadding)

  本例演示如何使用 Cell padding 来创建单元格内容与其边框之间的空白。

- [单元格间距(Cell spacing)](http://www.w3school.com.cn/tiy/t.asp?f=html_table_cellspacing)

  本例演示如何使用 Cell spacing 增加单元格之间的距离。

- [向表格添加背景颜色或背景图像](http://www.w3school.com.cn/tiy/t.asp?f=html_table_background)

  本例演示如何向表格添加背景。

- [向表格单元添加背景颜色或者背景图像](http://www.w3school.com.cn/tiy/t.asp?f=html_table_cellbackground)

  本例演示如何向一个或者更多表格单元添加背景。

- [在表格单元中排列内容](http://www.w3school.com.cn/tiy/t.asp?f=html_table_align)

  本例演示如何使用 "align" 属性排列单元格内容,以便创建一个美观的表格。

- [框架(frame)属性](http://www.w3school.com.cn/tiy/t.asp?f=html_table_frame)

  本例演示如何使用 "frame" 属性来控制围绕表格的边框。

## 表格标签

```
<table>	定义表格
<caption>	定义表格标题。
<th>	定义表格的表头。
<tr>	定义表格的行。
<td>	定义表格单元。
<thead>	定义表格的页眉。
<tbody>	定义表格的主体。
<tfoot>	定义表格的页脚。
<col>	定义用于表格列的属性。
<colgroup>	定义表格列的组。
```

