## 对带有指定属性的 HTML 元素设置样式。

可以为拥有指定属性的 HTML 元素设置样式，而不仅限于 class 和 id 属性。

注释：只有在规定了 !DOCTYPE 时，IE7 和 IE8 才支持属性选择器。在 IE6 及更低的版本中，不支持属性选择。

## 属性选择器

下面的例子为带有 title 属性的所有元素设置样式：

```
[title]
{
color:red;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_att)

## 属性和值选择器

下面的例子为 title="W3School" 的所有元素设置样式：

```
[title=W3School]
{
border:5px solid blue;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_value)

## 属性和值选择器 - 多个值

下面的例子为包含指定值的 title 属性的所有元素设置样式。适用于由空格分隔的属性值：

```
[title~=hello] { color:red; }
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_valuelist_space)

下面的例子为带有包含指定值的 lang 属性的所有元素设置样式。适用于由连字符分隔的属性值：

```
[lang|=en] { color:red; }
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_valuelist_hyphen)

## 设置表单的样式

属性选择器在为不带有 class 或 id 的表单设置样式时特别有用：

```
input[type="text"]
{
  width:150px;
  display:block;
  margin-bottom:10px;
  background-color:yellow;
  font-family: Verdana, Arial;
}

input[type="button"]
{
  width:120px;
  margin-left:35px;
  display:block;
  font-family: Verdana, Arial;
}

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_form)

## CSS 选择器参考手册

| 选择器                                                       | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [[*attribute*\]](http://www.w3school.com.cn/cssref/selector_attribute.asp) | 用于选取带有指定属性的元素。                                 |
| [[*attribute*=*value*\]](http://www.w3school.com.cn/cssref/selector_attribute_value.asp) | 用于选取带有指定属性和值的元素。                             |
| [[*attribute*~=*value*\]](http://www.w3school.com.cn/cssref/selector_attribute_value_contain.asp) | 用于选取属性值中包含指定词汇的元素。                         |
| [[*attribute*\|=*value*\]](http://www.w3school.com.cn/cssref/selector_attribute_value_start.asp) | 用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。 |
| [[*attribute*^=*value*\]](http://www.w3school.com.cn/cssref/selector_attr_begin.asp) | 匹配属性值以指定值开头的每个元素。                           |
| [[*attribute*$=*value*\]](http://www.w3school.com.cn/cssref/selector_attr_end.asp) | 匹配属性值以指定值结尾的每个元素。                           |
| [[*attribute**=*value*\]](http://www.w3school.com.cn/cssref/selector_attr_contain.asp) | 匹配属性值中包含指定值的每个元素。                           |

- [CSS 类选择器](http://www.w3school.com.cn/css/css_syntax_class_selector.asp)
- [CSS 创建](http://www.w3school.com.cn/css/css_howto.asp)

## 相关内容

如果您需要更深入地学习关于属性选择器的知识，请阅读 W3School 的高级教程：[CSS 属性选择器详解](http://www.w3school.com.cn/css/css_selector_attribute.asp)。