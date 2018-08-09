**Server-Sent 事件允许网页从服务器获得更新。**

## Server-Sent 事件 - One Way Messaging

Server-Sent 事件指的是网页自动从服务器获得更新。

以前也可能做到这一点，前提是网页不得不询问是否有可用的更新。通过 Server-Sent 事件，更新能够自动到达。

例如：Facebook/Twitter 更新、股价更新、新的博文、赛事结果，等等。

## 浏览器支持

表格中的数字指示完全支持 server-sent 事件的首个浏览器。

| API  |      |      |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| SSE  | 6.0  | 不支持  | 6.0  | 5.0  | 11.5 |

## 接收 Server-Sent 事件通知

EventSource 对象用于接收服务器发送事件通知：

### 实例

```
var source = new EventSource("demo_sse.php");
source.onmessage = function(event) {
    document.getElementById("result").innerHTML += event.data + "<br>";
};

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html5_sse)

### 例子解释：

- 创建一个新的 EventSource 对象，然后规定发送更新的页面的 URL（本例中是 "demo_sse.php"）
- 每当接收到一次更新，就会发生 onmessage 事件
- 当 onmessage 事件发生时，把已接收的数据推入 id 为 "result" 的元素中

## 检测 Server-Sent 事件支持

在 TIY 实例中，我们编写了一段额外的代码来检测服务器发送事件的浏览器支持：

```
if(typeof(EventSource) !== "undefined") {
    // 是的！支持服务器发送事件！
    // 一些代码.....
} else {
    // 抱歉！不支持服务器发送事件！
}

```

## 服务器端代码实例

为了使上例运行，您需要能够发送数据更新的服务器（比如 PHP 或 ASP）。

服务器端事件流的语法非常简单。请把 "Content-Type" 报头设置为 "text/event-stream"。现在，您可以开始发送事件流了。

```
PHP 中的代码 (demo_sse.php)：

<?php
header('Content-Type: text/event-stream');
header('Cache-Control: no-cache');

$time = date('r');
echo "data: The server time is: {$time}\n\n";
flush();
?>

ASP 中的代码 (VB) (demo_sse.asp)：

<%
Response.ContentType = "text/event-stream"
Response.Expires = -1
Response.Write("data: The server time is: " & now())
Response.Flush()
%>

```

### 代码解释：

- 把报头 "Content-Type" 设置为 "text/event-stream"
- 规定不对页面进行缓存
- 输出要发送的日期（始终以 "data: " 开头）
- 向网页刷新输出数据

## EventSource 对象

在上例中，我们使用 onmessage 事件来获取消息。不过还可以使用其他事件：

| 事件        | 描述           |
| --------- | ------------ |
| onopen    | 当通往服务器的连接被打开 |
| onmessage | 当接收到消息       |
| onerror   | 当发生错误        |