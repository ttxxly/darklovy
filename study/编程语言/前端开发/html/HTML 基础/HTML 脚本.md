**JavaScript 使 HTML 页面具有更强的动态和交互性。。**

## 实例

- [插入一段脚本](http://www.w3school.com.cn/tiy/t.asp?f=html_script)

  如何将脚本插入 HTML 文档。

- [使用  标签](http://www.w3school.com.cn/tiy/t.asp?f=html_noscript)

  如何应对不支持脚本或禁用脚本的浏览器。

## HTML script 元素

<script> 标签用于定义客户端脚本，比如 JavaScript。

script 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。

必需的 type 属性规定脚本的 MIME 类型。

JavaScript 最常用于图片操作、表单验证以及内容动态更新。

下面的脚本会向浏览器输出“Hello World!”：

```
<script type="text/javascript">
document.write("Hello World!")
</script>

```

提示：如果需要学习更多有关在 HTML 中编写脚本的知识，请访问我们的 [JavaScript 教程](http://www.w3school.com.cn/js/index.asp)。

## <noscript> 标签

<noscript> 标签提供无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。

noscript 元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。

只有在浏览器不支持脚本或者禁用脚本时，才会显示 noscript 元素中的内容：

```
<script type="text/javascript">
document.write("Hello World!")
</script>
<noscript>Your browser does not support JavaScript!</noscript>

```

## 如何应付老式的浏览器

如果浏览器压根没法识别 <script> 标签，那么 <script> 标签所包含的内容将以文本方式显示在页面上。为了避免这种情况发生，你应该将脚本隐藏在注释标签当中。那些老的浏览器（无法识别 <script> 标签的浏览器）将忽略这些注释，所以不会将标签的内容显示到页面上。而那些新的浏览器将读懂这些脚本并执行它们，即使代码被嵌套在注释标签内。

### 实例

#### JavaScript:

```
<script type="text/javascript">
<!--
document.write("Hello World!")
//-->
</script>

```

#### VBScript:

```
<script type="text/vbscript">
<!--
document.write("Hello World!")
'-->
</script>
```

| 标签                                       | 描述                   |
| ---------------------------------------- | -------------------- |
| [<script>](http://www.w3school.com.cn/tags/tag_script.asp) | 定义客户端脚本。             |
| [<noscript>](http://www.w3school.com.cn/tags/tag_noscript.asp) | 为不支持客户端脚本的浏览器定义替代内容。 |