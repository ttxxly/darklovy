`<label>` 标签为 input 元素定义标注（标记）。

label 元素不会向用户呈现任何特殊效果。如果您在 label 元素内点击文本，就会触发此控件。就是说，当用户选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。

`<label>` 标签的 for 属性应当与相关元素的 id 属性相同时，才有效果。

#### 标签属性

| 属性                                                       | 值       | 描述                                  |
| ---------------------------------------------------------- | -------- | ------------------------------------- |
| [for](http://www.w3school.com.cn/tags/att_label_for.asp)   | *id*     | 规定 label 绑定到哪个表单元素。       |
| [form](http://www.w3school.com.cn/tags/att_label_form.asp) | *formid* | 规定 label 字段所属的一个或多个表单。 |

*注：`label`标签支持HTML中的全局属性和事件属性*

#### 示例：

```
<form>
  <label for="male">Male</label>
  <input type="radio" name="sex" id="male" />
  <br />
  <label for="female">Female</label>
  <input type="radio" name="sex" id="female" />
</form>
```

发表于

```
https://blog.csdn.net/jdliyao/article/details/80011809
```

