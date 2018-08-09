**<object> 的作用是支持 HTML 助手（插件）。**

## HTML 助手（插件）

辅助应用程序（helper application）是可由浏览器启动的程序。辅助应用程序也称为插件。

辅助程序可用于播放音频和视频（以及其他）。辅助程序是使用 <object> 标签来加载的。

使用辅助程序播放视频和音频的一个优势是，您能够允许用户来控制部分或全部播放设置。

大多数辅助应用程序允许对音量设置和播放功能（比如后退、暂停、停止和播放）的手工（或程序的）控制。

## 在 HTML 中播放视频的最好方式？

如需了解在 HTML 中包含音视频的最好方法，请参阅下一章节。

## 使用 QuickTime 来播放 Wave 音频

实例

```
<object width="420" height="360"
classid="clsid:02BF25D5-8C17-4B23-BC80-D3488ABDDC6B"
codebase="http://www.apple.com/qtactivex/qtplugin.cab">
<param name="src" value="bird.wav" />
<param name="controller" value="true" />
</object>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_object_qtaudio)

## 使用 QuickTime 来播放 MP4 视频

实例

```
<object width="420" height="360"
classid="clsid:02BF25D5-8C17-4B23-BC80-D3488ABDDC6B"
codebase="http://www.apple.com/qtactivex/qtplugin.cab">
<param name="src" value="movie.mp4" />
<param name="controller" value="true" />
</object>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_object_qtvideo)

## 使用 Flash 来播放 SWF 视频

实例

```
<object width="400" height="40"
classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000"
codebase="http://fpdownload.macromedia.com/
pub/shockwave/cabs/flash/swflash.cab#version=8,0,0,0">
<param name="SRC" value="bookmark.swf">
<embed src="bookmark.swf" width="400" height="40"></embed>
</object>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_object_flash)

## 使用 Windows Media Player 来播放 WMV 影片

下面的例子展示用于播放 Windows 媒体文件的推荐代码：

实例

```
<object width="100%" height="100%"
type="video/x-ms-asf" url="3d.wmv" data="3d.wmv"
classid="CLSID:6BF52A52-394A-11d3-B153-00C04F79FAA6">
<param name="url" value="3d.wmv">
<param name="filename" value="3d.wmv">
<param name="autostart" value="1">
<param name="uiMode" value="full" />
<param name="autosize" value="1">
<param name="playcount" value="1">
<embed type="application/x-mplayer2" src="3d.wmv" width="100%"
 height="100%" autostart="true" showcontrols="true" 
pluginspage="http://www.microsoft.com/Windows/MediaPlayer/"></embed>
</object>

```

[亲自试一试](http://www.w3school.com.cn/tiy/t.asp?f=html_object_mplayer)