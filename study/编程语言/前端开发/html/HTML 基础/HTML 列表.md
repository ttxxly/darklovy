**HTML 支持有序、无序和定义列表**

## 实例

- [无序列表](http://www.w3school.com.cn/tiy/t.asp?f=html_list_unordered)

  本例演示无序列表。

- [有序列表](http://www.w3school.com.cn/tiy/t.asp?f=html_list_ordered)

  本例演示有序列表。

（[可以在本页底端找到更多实例](http://www.w3school.com.cn/html/html_lists.asp#more_examples)。）

## 无序列表

无序列表是一个项目的列表，此列项目使用粗体圆点（典型的小黑圆圈）进行标记。

无序列表始于 <ul> 标签。每个列表项始于 <li>。

```
<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>

```

浏览器显示如下：

- Coffee
- Milk

列表项内部可以使用段落、换行符、图片、链接以及其他列表等等。

## 有序列表

同样，有序列表也是一列项目，列表项目使用数字进行标记。

有序列表始于 <ol> 标签。每个列表项始于 <li> 标签。

```
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>

```

浏览器显示如下：

1. Coffee
2. Milk

列表项内部可以使用段落、换行符、图片、链接以及其他列表等等。

## 定义列表

自定义列表不仅仅是一列项目，而是项目及其注释的组合。

自定义列表以 <dl> 标签开始。每个自定义列表项以 <dt> 开始。每个自定义列表项的定义以 <dd> 开始。

```
<dl>
<dt>Coffee</dt>
<dd>Black hot drink</dd>
<dt>Milk</dt>
<dd>White cold drink</dd>
</dl>

```

浏览器显示如下：

- Coffee

  Black hot drink

- Milk

  White cold drink

定义列表的列表项内部可以使用段落、换行符、图片、链接以及其他列表等等。

## [更多实例]()

- [不同类型的无序列表](http://www.w3school.com.cn/tiy/t.asp?f=html_lists_unordered)

  本例演示一个无序列表。

- [不同类型的有序列表](http://www.w3school.com.cn/tiy/t.asp?f=html_lists_ordered)

  本例演示不同类型的有序列表。

- [嵌套列表](http://www.w3school.com.cn/tiy/t.asp?f=html_lists_nested)

  本例演示如何嵌套列表。

- [嵌套列表 2](http://www.w3school.com.cn/tiy/t.asp?f=html_lists_nested2)

  本例演示更复杂的嵌套列表。

- [定义列表](http://www.w3school.com.cn/tiy/t.asp?f=html_list_definition)

  本例演示一个定义列表。

## 列表标签

| 标签                                       | 描述               |
| ---------------------------------------- | ---------------- |
| [<ol>](http://www.w3school.com.cn/tags/tag_ol.asp) | 定义有序列表。          |
| [<ul>](http://www.w3school.com.cn/tags/tag_ul.asp) | 定义无序列表。          |
| [<li>](http://www.w3school.com.cn/tags/tag_li.asp) | 定义列表项。           |
| [<dl>](http://www.w3school.com.cn/tags/tag_dl.asp) | 定义定义列表。          |
| [<dt>](http://www.w3school.com.cn/tags/tag_dt.asp) | 定义定义项目。          |
| [<dd>](http://www.w3school.com.cn/tags/tag_dd.asp) | 定义定义的描述。         |
| [<dir>](http://www.w3school.com.cn/tags/tag_dir.asp) | 已废弃。使用 <ul> 代替它。 |
| [<menu>](http://www.w3school.com.cn/tags/tag_menu.asp) | 已废弃。使用 <ul> 代替它。 |