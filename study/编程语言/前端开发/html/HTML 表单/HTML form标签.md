所有浏览器都支持 `<form>` 标签。

`<form>` 标签用于为用户输入创建 HTML 表单。

表单能够包含 `input`元素，比如文本字段、复选框、单选框、提交按钮等等。

表单还可以包含 `menus`、`textarea`、`fieldset`、`legend` 和 `label` 元素。

表单用于向服务器传输数据。

**`form` 元素是块级元素，其前后会产生折行**

#### 相关属性

| 属性                                                         | 值                                | 描述                                     |
| ------------------------------------------------------------ | --------------------------------- | ---------------------------------------- |
| accept                                                       | *MIME_type*                       | HTML 5 中不支持。                        |
| [accept-charset](http://www.w3school.com.cn/tags/att_form_accept-charset.asp) | *charset_list*                    | 规定服务器可处理的表单数据字符集。       |
| [action](http://www.w3school.com.cn/tags/att_form_action.asp) | *URL*                             | 规定当提交表单时向何处发送表单数据。     |
| [autocomplete](http://www.w3school.com.cn/tags/att_form_autocomplete.asp) | onoff                             | 规定是否启用表单的自动完成功能。         |
| [enctype](http://www.w3school.com.cn/tags/att_form_enctype.asp) | 见说明                            | 规定在发送表单数据之前如何对其进行编码。 |
| [method](http://www.w3school.com.cn/tags/att_form_method.asp) | getpost                           | 规定用于发送 form-data 的 HTTP 方法。    |
| [name](http://www.w3school.com.cn/tags/att_form_name.asp)    | *form_name*                       | 规定表单的名称。                         |
| [novalidate](http://www.w3school.com.cn/tags/att_form_novalidate.asp) | novalidate                        | 如果使用该属性，则提交表单时不进行验证。 |
| [target](http://www.w3school.com.cn/tags/att_form_target.asp) | _blank_self_parent_top*framename* | 规定在何处打开 action URL。              |

*注：支持 HTML 的全局属性和事件属性*

#### 示例

```
<form action="form_action.asp" method="get">
  <p>First name: <input type="text" name="fname" /></p>
  <p>Last name: <input type="text" name="lname" /></p>
  <input type="submit" value="Submit" />
</form>
```

[戳我查看HTML的全局属性](https://blog.csdn.net/jdliyao/article/details/80011899)

[戳我查看HTML的事件属性](https://blog.csdn.net/jdliyao/article/details/80012046)

发表于：

```
https://blog.csdn.net/jdliyao/article/details/80012211
微信公众号 - xlLoveLove
```

