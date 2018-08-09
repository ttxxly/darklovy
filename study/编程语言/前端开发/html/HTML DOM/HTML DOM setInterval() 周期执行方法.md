setInterval()方法可按照指定的周期（以毫秒计）来调用函数或计算表达式。

setInterval()方法会不停地调用函数，直到clearInterval()被调用或者窗口被关闭。它的值可以被用作clearInterval()方法的参数。

#### 语法

```
setInterval(code, milliseconds);
setInterval(function, milliseconds, param1, param2, ...)

code/function	必需。要调用一个代码串，也可以是一个函数。
milliseconds	必须。周期性执行或调用 code/function 之间的时间间隔，以毫秒计。
param1, param2, ...	可选。 传给执行函数的其他参数（IE9 及其更早版本不支持该参数）。

返回值：可以传递给 window.clearInterval() 方法，从而取消对 code 的周期性执行。
```

#### 示例

```
<html>
<style>
	body{text-align: center}
</style>
<body>

<input type="text" id="clock" size="35" />
<script language=javascript>
var int=self.setInterval("clock()",50)
function clock()
  {
  var t=new Date()
  document.getElementById("clock").value=t
  }
</script>
</form>
<button onclick="int=window.clearInterval(int)">
Stop interval</button>

</body>
</html>
```

参考资料：

* http://www.jb51.net/shouce/htmldom/jb51.net.htmldom/htmldom/met_win_setinterval.asp.html
* http://www.runoob.com/jsref/met-win-setinterval.html