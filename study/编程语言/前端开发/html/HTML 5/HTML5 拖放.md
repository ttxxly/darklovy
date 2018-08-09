## 拖放

拖放（Drag 和 Drop）是很常见的特性。它指的是您抓取某物并拖入不同的位置。

拖放是 HTML5 标准的组成部分：任何元素都是可拖放的。

## 浏览器支持

表格中的数字指示了完全支持拖放的首个浏览器版本。

| API  |      |      |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 拖放   | 4.0  | 9.0  | 3.5  | 6.0  | 12.0 |

## HTML 拖放实例

下列是关于拖放的简单例子：

### 实例

```
<!DOCTYPE HTML>
<html>
<head>
<script>
function allowDrop(ev) {
    ev.preventDefault();
}

function drag(ev) {
    ev.dataTransfer.setData("text", ev.target.id);
}

function drop(ev) {
    ev.preventDefault();
    var data = ev.dataTransfer.getData("text");
    ev.target.appendChild(document.getElementById(data));
}
</script>
</head>
<body>

<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>

<img id="drag1" src="img_logo.gif" draggable="true" ondragstart="drag(event)" width="336" height="69">

</body>
</html>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_draganddrop)

它也许看上去有点复杂，不过让我们研究一下拖放事件的所有不同部分。

## 把元素设置为可拖放

首先：为了把一个元素设置为可拖放，请把 draggable 属性设置为 true：

```
<img draggable="true">
```

## 拖放的内容 - ondragstart 和 setData()

然后，规定当元素被拖动时发生的事情。

在上面的例子中，ondragstart 属性调用了一个 drag(event) 函数，规定拖动什么数据。

dataTransfer.setData() 方法设置被拖动数据的数据类型和值：

```
function drag(ev) {
    ev.dataTransfer.setData("text", ev.target.id);
}

```

在本例中，数据类型是 "text"，而值是这个可拖动元素的 id ("drag1")。

## 拖到何处 - ondragover

ondragover 事件规定被拖动的数据能够被放置到何处。

默认地，数据/元素无法被放置到其他元素中。为了实现拖放，我们必须阻止元素的这种默认的处理方式。

这个任务由 ondragover 事件的 event.preventDefault() 方法完成：

```
event.preventDefault()
```

## 进行放置 - ondrop

当放开被拖数据时，会发生 drop 事件。

在上面的例子中，ondrop 属性调用了一个函数，drop(event)：

```
function drop(ev) {
    ev.preventDefault();
    var data = ev.dataTransfer.getData("text");
    ev.target.appendChild(document.getElementById(data));
}

```

### 代码解释：

- 调用 preventDefault() 来阻止数据的浏览器默认处理方式（drop 事件的默认行为是以链接形式打开）
- 通过 dataTransfer.getData() 方法获得被拖的数据。该方法将返回在 setData() 方法中设置为相同类型的任何数据
- 被拖数据是被拖元素的 id ("drag1")
- 把被拖元素追加到放置元素中

## 更多实例

### 来回拖放图片

如何在两个 <div> 元素之间来回拖放图像：

![img](http://www.w3school.com.cn/i/eg_dragdrop_w3school.gif)

请把 W3School 图片拖到矩形中。

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_draganddrop2)