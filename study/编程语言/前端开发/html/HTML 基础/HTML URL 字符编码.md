**URL 编码会将字符转换为可通过因特网传输的格式。**

## URL - 统一资源定位器

Web 浏览器通过 URL 从 web 服务器请求页面。

URL 是网页的地址，比如 *http://www.w3school.com.cn*。

## URL 编码

URL 只能使用 [ASCII 字符集](http://www.w3school.com.cn/tags/html_ref_ascii.asp)来通过因特网进行发送。

由于 URL 常常会包含 ASCII 集合之外的字符，URL 必须转换为有效的 ASCII 格式。

URL 编码使用 "%" 其后跟随两位的十六进制数来替换非 ASCII 字符。

URL 不能包含空格。URL 编码通常使用 + 来替换空格。

## 亲自试一试

如果您点击下面的“提交”按钮，浏览器会在发送输入之前对其进行 URL 编码。服务器上的页面会显示出接收到的输入。

 

试着输入一些字符，然后再次点击提交按钮。

## URL 编码示例

| 字符   | URL 编码 |
| ---- | ------ |
| €    | %80    |
| £    | %A3    |
| ©    | %A9    |
| ®    | %AE    |
| À    | %C0    |
| Á    | %C1    |
| Â    | %C2    |
| Ã    | %C3    |
| Ä    | %C4    |
| Å    | %C5    |

如需完整的 URL 编码参考，请访问我们的 [URL 编码参考手册](http://www.w3school.com.cn/tags/html_ref_urlencode.html)。