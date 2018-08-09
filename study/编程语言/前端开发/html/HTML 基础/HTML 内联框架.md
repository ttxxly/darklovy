**iframe 用于在网页内显示网页。**

## 添加 iframe 的语法

```
<iframe src="URL"></iframe>
```

*URL* 指向隔离页面的位置。

## Iframe - 设置高度和宽度

height 和 width 属性用于规定 iframe 的高度和宽度。

属性值的默认单位是像素，但也可以用百分比来设定（比如 "80%"）。

### 实例

```
<iframe src="demo_iframe.htm" width="200" height="200"></iframe>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_iframe_height_width)

## Iframe - 删除边框

frameborder 属性规定是否显示 iframe 周围的边框。

设置属性值为 "0" 就可以移除边框：

### 实例

```
<iframe src="demo_iframe.htm" frameborder="0"></iframe>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_iframe_frameborder)

## 使用 iframe 作为链接的目标

iframe 可用作链接的目标（target）。

链接的 target 属性必须引用 iframe 的 name 属性：

### 实例

```
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="http://www.w3school.com.cn" target="iframe_a">W3School.com.cn</a></p>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_iframe_target)

## HTML iframe 标签

| 标签                                       | 描述           |
| ---------------------------------------- | ------------ |
| [<iframe>](http://www.w3school.com.cn/tags/tag_iframe.asp) | 定义内联的子窗口（框架） |