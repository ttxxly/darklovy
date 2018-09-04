---
title: eclipse 安装与配置
date: 2018-08-06 16:30:33
tags: Java
---

下载链接： http://www.eclipse.org/downloads/eclipse-packages/

<!--more-->

eclipse配置

```
1. 配置工作空间的编码格式 window -> preference ->  General -> Workspace
	-> Text File encoding
2. eclipse 配置 Tomcat 服务器
	window -> preference -> server -> Runtime environment
	-> add
3. Java 代码自动提示
	Window > Preferences > Java > Editor > Content Assist
	“Auto Activation triggers for java”这个选项就是指触发代码提示的的选项，
     把“.”修改成".abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"
4. XML 代码自动提示
	Window > Preferences > Xml > Xml Files > Editor > Content Assist > 
	Auto activation > Prompt when these characters are inserted ，设置框中默认是 <=: ，
	改为： <=:.abcdefghijklmnopqrstuvwxyz(,
```

感兴趣的话可以点击下面的链接，关注我的微信公众号和我的知识星球。

> https://www.ttxxly.top/images/qrcode_darklovy.jpg
>
> https://www.ttxxly.top/images/qrcode_ttxxly123.jpg
>
> https://www.ttxxly.top/images/ZSXQ_darklovy.png

