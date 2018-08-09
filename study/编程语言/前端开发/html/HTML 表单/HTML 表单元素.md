**本章描述所有 HTML 表单元素。**

## <input> 元素

最重要的表单元素是 *<input>* 元素。

<input> 元素根据不同的 *type* 属性，可以变化为多种形态。

注释：下一章讲解所有 HTML 输入类型。

## <select> 元素（下拉列表）

*<select>* 元素定义*下拉列表*：

### 实例

```
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_elements_select)

*<option>* 元素定义待选择的选项。

列表通常会把首个选项显示为被选选项。

您能够通过添加 selected 属性来定义预定义选项。

### 实例

```
<option value="fiat" selected>Fiat</option>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_elements_select_pre)

## <textarea> 元素

*<textarea>* 元素定义多行输入字段（*文本域*）：

### 实例

```
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_headers)

以上 HTML 代码在浏览器中显示为：

```
The cat was playing in the garden.
```

## <button> 元素

*<button>* 元素定义可点击的*按钮*：

### 实例

```
<button type="button" onclick="alert('Hello World!')">Click Me!</button>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_elements_button)

以上 HTML 代码在浏览器中显示为：

## HTML5 表单元素

HTML5 增加了如下表单元素：

- <datalist>
- <keygen>
- <output>

注释：默认地，浏览器不会显示未知元素。新元素不会破坏您的页面。

## HTML5 <datalist> 元素

*<datalist>* 元素为 <input> 元素规定预定义选项列表。

用户会在他们输入数据时看到预定义选项的下拉列表。

<input> 元素的 *list* 属性必须引用 <datalist> 元素的 *id* 属性。

### 实例

通过 <datalist> 设置预定义值的 <input> 元素：

```
<form action="action_page.php">
<input list="browsers">
<datalist id="browsers">
   <option value="Internet Explorer">
   <option value="Firefox">
   <option value="Chrome">
   <option value="Opera">
   <option value="Safari">
</datalist> 
</form>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_elements_datalist)