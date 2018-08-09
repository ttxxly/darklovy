计算机代码

```
var person = {
    firstName:"Bill",
    lastName:"Gates",
    age:50,
    eyeColor:"blue"
}
```

## HTML 计算机代码格式

通常，HTML 使用*可变*的字母尺寸，以及可变的字母间距。

在显示*计算机代码*示例时，并不需要如此。

*<kbd>*, *<samp>*, 以及 *<code>* 元素全都支持固定的字母尺寸和间距。

## HTML 键盘格式

HTML *<kbd>* 元素定义*键盘输入*：

### 实例

```
<p>To open a file, select:</p>

<p><kbd>File | Open...</kbd></p>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_kbd)

## HTML 样本格式

HTML *<samp>* 元素定义*计算机输出示例*：

### 实例

```
<samp>
demo.example.com login: Apr 12 09:10:17
Linux 2.6.10-grsec+gg3+e+fhs6b+nfs+gr0501+++p3+c4a+gr2b-reslog-v6.189
</samp>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_samp)

## HTML 代码格式

HTML *<code>* 元素定义*编程代码示例*：

### 实例

```
<code>
var person = { firstName:"Bill", lastName:"Gates", age:50, eyeColor:"blue" }
</code>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_code)

<code> 元素*不保留*多余的*空格*和*折行*：

### 实例

```
<p>Coding Example:</p>

<code>
var person = {
    firstName:"Bill",
    lastName:"Gates",
    age:50,
    eyeColor:"blue"
}
</code>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_codelines)

如需解决该问题，您必须在 <pre> 元素中包围代码：

### 实例

```
<p>Coding Example:</p>

<code>
<pre>
var person = {
    firstName:"Bill",
    lastName:"Gates",
    age:50,
    eyeColor:"blue"
}
</pre>
</code>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_codepre)

## HTML 变量格式化

HTML *<var>* 元素定义*数学变量*：

### 实例

```
<p>Einstein wrote:</p>

<p><var>E = m c<sup>2</sup></var></p>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_formatting_var)

## HTML 计算机代码元素

| 标签     | 描述        |
| ------ | --------- |
| <code> | 定义计算机代码文本 |
| <kbd>  | 定义键盘文本    |
| <samp> | 定义计算机代码示例 |
| <var>  | 定义变量      |
| <pre>  | 定义预格式化文本  |
