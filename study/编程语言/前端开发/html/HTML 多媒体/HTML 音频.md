**在 HTML 中播放声音的方法有很多种。**

## 问题，问题，以及解决方法

在 HTML 中播放音频并不容易！

您需要谙熟大量技巧，以确保您的音频文件在所有浏览器中（Internet Explorer, Chrome, Firefox, Safari, Opera）和所有硬件上（PC, Mac , iPad, iPhone）都能够播放。

在本章，W3School 为您总结了问题和解决方法。

## 使用插件

浏览器插件是一种扩展浏览器标准功能的小型计算机程序。

插件有很多用途：播放音乐、显示地图、验证银行账号，控制输入等等。

可使用 <object> 或 <embed> 标签来将插件添加到 HTML 页面。

这些标签定义资源（通常非 HTML 资源）的容器，根据类型，它们即会由浏览器显示，也会由外部插件显示。

## 使用 <embed> 元素

<embed> 标签定义外部（非 HTML）内容的容器。（这是一个 HTML5 标签，在 HTML4 中是非法的，但是所有浏览器中都有效）。

下面的代码片段能够显示嵌入网页中的 MP3 文件：

### 实例

```
<embed height="100" width="100" src="song.mp3" />
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_audio_embed)

### 问题：

- <embed> 标签在 HTML 4 中是无效的。页面无法通过 HTML 4 验证。
- 不同的浏览器对音频格式的支持也不同。
- 如果浏览器不支持该文件格式，没有插件的话就无法播放该音频。
- 如果用户的计算机未安装插件，无法播放音频。
- 如果把该文件转换为其他格式，仍然无法在所有浏览器中播放。

注释：使用 <!DOCTYPE html> (HTML5) 解决验证问题。

## 使用 <object> 元素

<object tag> 标签也可以定义外部（非 HTML）内容的容器。

下面的代码片段能够显示嵌入网页中的 MP3 文件：

### 实例

```
<object height="100" width="100" data="song.mp3"></object>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_audio_object)

### 问题：

- 不同的浏览器对音频格式的支持也不同。
- 如果浏览器不支持该文件格式，没有插件的话就无法播放该音频。
- 如果用户的计算机未安装插件，无法播放音频。
- 如果把该文件转换为其他格式，仍然无法在所有浏览器中播放。

## 使用 HTML5 <audio> 元素

<audio> 元素是一个 HTML5 元素，在 HTML 4 中是非法的，但在所有浏览器中都有效。

### 实例

```
<audio controls="controls">
  <source src="song.mp3" type="audio/mp3" />
  <source src="song.ogg" type="audio/ogg" />
Your browser does not support this audio format.
</audio>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_audio_html5)

上面的例子使用了一个 mp3 文件，这样它在 Internet Explorer、Chrome 以及 Safari 中是有效的。

为了使这段音频在 Firefox 和 Opera 中同样有效，添加了一个 ogg 类型的文件。如果失败，会显示错误消息。

### 问题：

- <audio> 标签在 HTML 4 中是无效的。您的页面无法通过 HTML 4 验证。
- 您必须把音频文件转换为不同的格式。
- <audio> 元素在老式浏览器中不起作用。

注释：使用 <!DOCTYPE html> (HTML5) 解决验证问题。

## 最好的 HTML 解决方法

### 实例

```
<audio controls="controls" height="100" width="100">
  <source src="song.mp3" type="audio/mp3" />
  <source src="song.ogg" type="audio/ogg" />
<embed height="100" width="100" src="song.mp3" />
</audio>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_audio_all)

上面的例子使用了两个不同的音频格式。HTML5 <audio> 元素会尝试以 mp3 或 ogg 来播放音频。如果失败，代码将回退尝试 <embed> 元素。

### 问题：

- 您必须把音频转换为不同的格式。
- <audio> 元素无法通过 HTML 4 和 XHTML 验证。
- <embed> 元素无法通过 HTML 4 和 XHTML 验证。
- <embed> 元素无法回退来显示错误消息。

注释：使用 <!DOCTYPE html> (HTML5) 解决验证问题。

## 向网站添加音频的最简单方法

向网页添加音频的最简单的方法是什么？

雅虎的媒体播放器绝对算其中之一。

使用雅虎媒体播放器是一个不同的途径。您只需简单地让雅虎来完成歌曲播放的工作就好了。

它能播放 mp3 以及一系列其他格式。通过一行简单的代码，您就可以把它添加到网页中，轻松地将 HTML 页面转变为专业的播放列表。

## 雅虎媒体播放器

### 实例

```
<a href="song.mp3">Play Sound</a>

<script type="text/javascript" src="http://mediaplayer.yahoo.com/js">
</script>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_audio_yahoo)

使用雅虎播放器是免费的。如需使用它，您需要把这段 JavaScript 插入网页底部：

```
<script type="text/javascript" src="http://mediaplayer.yahoo.com/js"></script>
```

然后只需简单地把 MP3 文件链接到您的 HTML 中，JavaScript 会自动地为每首歌创建播放按钮：

```
<a href="song1.mp3">Play Song 1</a>
<a href="song2.mp3">Play Song 2</a>
...
...
...

```

雅虎媒体播放器为您的用户提供的是一个小型的播放按钮，而不是完整的播放器。不过，当您点击该按钮，会弹出完整的播放器。

请注意，这个播放器始终停靠在窗框底部。只需点击它，就可将其滑出。

## 使用超链接

如果网页包含指向媒体文件的超链接，大多数浏览器会使用“辅助应用程序”来播放文件。

以下代码片段显示指向 mp3 文件的链接。如果用户点击该链接，浏览器会启动“辅助应用程序”来播放该文件：

### 实例

```
<a href="song.mp3">Play the sound</a>
```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_audio_link)

## 内联的声音

当您在网页中包含声音，或者作为网页的组成部分时，它被称为内联声音。

如果您打算在 web 应用程序中使用内联声音，您需要意识到很多人都觉得内联声音令人恼火。同时请注意，用户可能已经关闭了浏览器中的内联声音选项。

我们最好的建议是只在用户希望听到内联声音的地方包含它们。一个正面的例子是，在用户需要听到录音并点击某个链接时，会打开页面然后播放录音。

## HTML 4.01 多媒体标签

| 标签                                       | 描述                           |
| ---------------------------------------- | ---------------------------- |
| [](http://www.w3school.com.cn/tags/tag_applet.asp) | 不赞成。定义内嵌 applet。             |
| <embed>                                  | HTML4 中不赞成，HTML5 中允许。定义内嵌对象。 |
| [](http://www.w3school.com.cn/tags/tag_object.asp) | 定义内嵌对象。                      |
| [](http://www.w3school.com.cn/tags/tag_param.asp) | 定义对象的参数。                     |

## HTML 5 多媒体标签

| 标签                                       | 描述                 |
| ---------------------------------------- | ------------------ |
| [](http://www.w3school.com.cn/tags/tag_audio.asp) | 标签定义声音，比如音乐或其他音频流。 |
| [](http://www.w3school.com.cn/tags/tag_embed.asp) | 标签定义嵌入的内容，比如插件。    |