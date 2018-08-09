请看如下的一份字符串：

```
data:image/gif;base64,R0lGODlhHAAmAKIHAKqqqsvLy0hISObm5vf394uLiwAAAP///yH5B…EoqQqJKAIBaQOVKHAXr3t7txgBjboSvB8EpLoFZywOAo3LFE....
```

现在我们需要是`base64,`后面的字符串：

```
截取方法：
	1. 先使用js中的 indexof 方法找到 ',' 字符的下标
	2. 使用 js 中的 substring 方法 直接截取 下标后面的值
	
	str.substring(str.indexof(',')+1)
```

