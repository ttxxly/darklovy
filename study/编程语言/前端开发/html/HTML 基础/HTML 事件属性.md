HTML 4 增加了使事件在浏览器中触发动作的能力，比如当用户点击元素时启动 JavaScript。

下面列出了添加到 HTML 元素以定义事件动作的全局事件属性。

#### Window 事件属性

针对 window 对象触发的事件（应用到 <body> 标签）：

| 属性                                       | 值      | 描述                        |
| ---------------------------------------- | ------ | ------------------------- |
| [onafterprint](http://www.w3school.com.cn/tags/event_onafterprint.asp) | script | 文档打印之后运行的脚本。              |
| [onbeforeprint](http://www.w3school.com.cn/tags/event_onbeforeprint.asp) | script | 文档打印之前运行的脚本。              |
| onbeforeunload                           | script | 文档卸载之前运行的脚本。              |
| onerror                                  | script | 在错误发生时运行的脚本。              |
| onhaschange                              | script | 当文档已改变时运行的脚本。             |
| [onload](http://www.w3school.com.cn/tags/event_onload.asp) | script | 页面结束加载之后触发。               |
| onmessage                                | script | 在消息被触发时运行的脚本。             |
| onoffline                                | script | 当文档离线时运行的脚本。              |
| ononline                                 | script | 当文档上线时运行的脚本。              |
| onpagehide                               | script | 当窗口隐藏时运行的脚本。              |
| onpageshow                               | script | 当窗口成为可见时运行的脚本。            |
| onpopstate                               | script | 当窗口历史记录改变时运行的脚本。          |
| onredo                                   | script | 当文档执行撤销（redo）时运行的脚本。      |
| [onresize](http://www.w3school.com.cn/tags/event_onresize.asp) | script | 当浏览器窗口被调整大小时触发。           |
| onstorage                                | script | 在 Web Storage 区域更新后运行的脚本。 |
| onundo                                   | script | 在文档执行 undo 时运行的脚本。        |
| [onunload](http://www.w3school.com.cn/tags/event_onunload.asp) | script | 一旦页面已下载时触发（或者浏览器窗口已被关闭）。  |

#### Form 事件

由 HTML 表单内的动作触发的事件（应用到几乎所有 HTML 元素，但最常用在 form 元素中）：

| 属性                                       | 值      | 描述                          |
| ---------------------------------------- | ------ | --------------------------- |
| [onblur](http://www.w3school.com.cn/tags/event_onblur.asp) | script | 元素失去焦点时运行的脚本。               |
| [onchange](http://www.w3school.com.cn/tags/event_onchange.asp) | script | 在元素值被改变时运行的脚本。              |
| oncontextmenu                            | script | 当上下文菜单被触发时运行的脚本。            |
| [onfocus](http://www.w3school.com.cn/tags/event_onfocus.asp) | script | 当元素获得焦点时运行的脚本。              |
| onformchange                             | script | 在表单改变时运行的脚本。                |
| onforminput                              | script | 当表单获得用户输入时运行的脚本。            |
| oninput                                  | script | 当元素获得用户输入时运行的脚本。            |
| oninvalid                                | script | 当元素无效时运行的脚本。                |
| onreset                                  | script | 当表单中的重置按钮被点击时触发。HTML5 中不支持。 |
| [onselect](http://www.w3school.com.cn/tags/event_onselect.asp) | script | 在元素中文本被选中后触发。               |
| [onsubmit](http://www.w3school.com.cn/tags/event_onsubmit.asp) | script | 在提交表单时触发。                   |

#### Keyboard 事件

| 属性                                       | 值      | 描述          |
| ---------------------------------------- | ------ | ----------- |
| [onkeydown](http://www.w3school.com.cn/tags/event_onkeydown.asp) | script | 在用户按下按键时触发。 |
| [onkeypress](http://www.w3school.com.cn/tags/event_onkeypress.asp) | script | 在用户敲击按钮时触发。 |
| [onkeyup](http://www.w3school.com.cn/tags/event_onkeyup.asp) | script | 当用户释放按键时触发。 |

#### Mouse 事件

由鼠标或类似用户动作触发的事件：

| 属性                                       | 值      | 描述                      |
| ---------------------------------------- | ------ | ----------------------- |
| [onclick](http://www.w3school.com.cn/tags/event_onclick.asp) | script | 元素上发生鼠标点击时触发。           |
| [ondblclick](http://www.w3school.com.cn/tags/event_ondblclick.asp) | script | 元素上发生鼠标双击时触发。           |
| ondrag                                   | script | 元素被拖动时运行的脚本。            |
| ondragend                                | script | 在拖动操作末端运行的脚本。           |
| ondragenter                              | script | 当元素元素已被拖动到有效拖放区域时运行的脚本。 |
| ondragleave                              | script | 当元素离开有效拖放目标时运行的脚本。      |
| ondragover                               | script | 当元素在有效拖放目标上正在被拖动时运行的脚本。 |
| ondragstart                              | script | 在拖动操作开端运行的脚本。           |
| ondrop                                   | script | 当被拖元素正在被拖放时运行的脚本。       |
| [onmousedown](http://www.w3school.com.cn/tags/event_onmousedown.asp) | script | 当元素上按下鼠标按钮时触发。          |
| [onmousemove](http://www.w3school.com.cn/tags/event_onmousemove.asp) | script | 当鼠标指针移动到元素上时触发。         |
| [onmouseout](http://www.w3school.com.cn/tags/event_onmouseout.asp) | script | 当鼠标指针移出元素时触发。           |
| [onmouseover](http://www.w3school.com.cn/tags/event_onmouseover.asp) | script | 当鼠标指针移动到元素上时触发。         |
| [onmouseup](http://www.w3school.com.cn/tags/event_onmouseup.asp) | script | 当在元素上释放鼠标按钮时触发。         |
| onmousewheel                             | script | 当鼠标滚轮正在被滚动时运行的脚本。       |
| onscroll                                 | script | 当元素滚动条被滚动时运行的脚本。        |

#### Media 事件

由媒介（比如视频、图像和音频）触发的事件（适用于所有 HTML 元素，但常见于媒介元素中，比如 <audio>、<embed>、<img>、<object> 以及 <video>）:

| 属性                 | 值      | 描述                                    |
| ------------------ | ------ | ------------------------------------- |
| onabort            | script | 在退出时运行的脚本。                            |
| oncanplay          | script | 当文件就绪可以开始播放时运行的脚本（缓冲已足够开始时）。          |
| oncanplaythrough   | script | 当媒介能够无需因缓冲而停止即可播放至结尾时运行的脚本。           |
| ondurationchange   | script | 当媒介长度改变时运行的脚本。                        |
| onemptied          | script | 当发生故障并且文件突然不可用时运行的脚本（比如连接意外断开时）。      |
| onended            | script | 当媒介已到达结尾时运行的脚本（可发送类似“感谢观看”之类的消息）。     |
| onerror            | script | 当在文件加载期间发生错误时运行的脚本。                   |
| onloadeddata       | script | 当媒介数据已加载时运行的脚本。                       |
| onloadedmetadata   | script | 当元数据（比如分辨率和时长）被加载时运行的脚本。              |
| onloadstart        | script | 在文件开始加载且未实际加载任何数据前运行的脚本。              |
| onpause            | script | 当媒介被用户或程序暂停时运行的脚本。                    |
| onplay             | script | 当媒介已就绪可以开始播放时运行的脚本。                   |
| onplaying          | script | 当媒介已开始播放时运行的脚本。                       |
| onprogress         | script | 当浏览器正在获取媒介数据时运行的脚本。                   |
| onratechange       | script | 每当回放速率改变时运行的脚本（比如当用户切换到慢动作或快进模式）。     |
| onreadystatechange | script | 每当就绪状态改变时运行的脚本（就绪状态监测媒介数据的状态）。        |
| onseeked           | script | 当 seeking 属性设置为 false（指示定位已结束）时运行的脚本。 |
| onseeking          | script | 当 seeking 属性设置为 true（指示定位是活动的）时运行的脚本。 |
| onstalled          | script | 在浏览器不论何种原因未能取回媒介数据时运行的脚本。             |
| onsuspend          | script | 在媒介数据完全加载之前不论何种原因终止取回媒介数据时运行的脚本。      |
| ontimeupdate       | script | 当播放位置改变时（比如当用户快进到媒介中一个不同的位置时）运行的脚本。   |
| onvolumechange     | script | 每当音量改变时（包括将音量设置为静音）时运行的脚本。            |
| onwaiting          | script | 当媒介已停止播放但打算继续播放时（比如当媒介暂停已缓冲更多数据）运行脚本  |

发表于：

```
https://blog.csdn.net/jdliyao/article/details/80012046
```

