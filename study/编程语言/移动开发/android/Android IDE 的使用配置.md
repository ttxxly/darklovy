**每次Android studio更新后都要修改配置文件我也是醉了**

# 配置Android studio本地项目提交到GitHub


* git版本控制系统
* 你需要一个GitHub账号


### 操作步骤

##### 关联Android studio和git

在 ```setting -> Version Control -> git -> Path to git executable``` 中选择你安装的GitGUI中 ```bin``` 目录下 ```git.exe```

路径选择好后，可以点击右边的 ```test``` ， 测试是否关联。

##### 关联Android studio 和 GitHub

在 ```setting -> Version Control -> Github``` 中 填入您的账号和密码， 然后点击 ```test```. 测试是否成功。

##### 上传项目

新建一个项目，然后选择 ```VCS -> import into Version Control -> share project on github``` 

1. 怎样只将我们想让它上传的部分上传，而不是全部上传?  
在 ```project``` 文件夹下有个 ```.gitignore``` 文件，这个文件就是控制那些文件不上传的。 在右上部分，会叫我们安装插件，安装就可以了。（操作在Android studio中进行）

2. 插件安装成功重启后，在打开这个文件后，还提醒我们安装？  
这个说明我们插件下载的目录可能不对，如果你自定义了Android studioode配置文件，请测试是否能够正确安装插件等。

下面是我的自定义配置文件:

```
#---------------------------------------------------------------------
# Uncomment this option if you want to customize path to IDE config folder. Make sure you're using forward slashes.
#---------------------------------------------------------------------
 idea.config.path=D:/development-tool/Android/AndroidStudioConfiguration/.AndroidStudio/config

#---------------------------------------------------------------------
# Uncomment this option if you want to customize path to IDE system folder. Make sure you're using forward slashes.
#---------------------------------------------------------------------
 idea.system.path=D:/development-tool/Android/AndroidStudioConfiguration/.AndroidStudio/system

#---------------------------------------------------------------------
# Uncomment this option if you want to customize path to user installed plugins folder. 
#Make sure you're using forward slashes.
#---------------------------------------------------------------------
 idea.plugins.path=${idea.system.path}/plugins
#特别注意这个的路径是 idea.system.path

#---------------------------------------------------------------------
# Uncomment this option if you want to customize path to IDE logs folder. Make sure you're using forward slashes.
#---------------------------------------------------------------------
 idea.log.path=${idea.system.path}/log
```

### 未完 哈哈， 不想写了 


# Android studio keyboard

##### 自动生成变量

eclipse： ctrl + 2, l   (先按 Ctrl 2， 在按 l)
Android studio： Ctrl alt v

##### 格式化代码

android studio : ctrl alt l

##### 参数提示

Android studio： Ctrl p

##### 列出所有的类、方法

eclipse: ctrl + o
android studio : alt + 7

##### 查看类的继承关系

Android studio： ctrl + h

##### 局部变全局、全局变局部

Android studio：
* 提升为全局变量： Ctrl Alt F
* 提升为局部变量： ctrl Alt V
* 提取方法：        ctrl Alt M

##### 删除行，删除并复制行，复制行并粘贴

Android studio： Ctrl + y、ctrl + x、ctrl + d

##### 调出当前文件的大纲，并通过模糊匹配快速跳转至指定的方法

Android studio：ctrl + f12

##### 查看某个方法的调用路径

Android studio：ctrl + alt + h

##### 快速查看某个方法或者类的实现。通过大概预览下调用的方法，可以避免许多未知的坑

Android studio：ctrl + shift + i

##### 书签，帮助快速回到指定的位置

f11 
将当前位置添加到书签中或者从书签中移除。

shift+f11 
显示有哪些书签。

##### 对于没有设置快捷键或者忘记快捷键的菜单或者动作（Action），可能通过输入其名字快速调用。神技！！！

Android studio：Ctrl + shift + a

##### 上下移动行

Android studio：alt + shift + up/down 

#### 快速提交代码、暂存代码、切分支等操作操作如鱼得水。

android studio: alt + `

##### 关闭或者恢复其他窗口。在编写代码的时候非常方便的全屏编辑框

android studio: ctrl + shift + f12

##### 重命名变量或者方法名

Android studio： shift + f6

##### 快速查看变量的值

按住Alt点击想要查看的变量或者语句。如果想查看更多，则可以按Alt+f8

##### 分析某个值的来源

Find Actions(ctrl+shift+a)输入"Analyze Data Flow to Here"，可以查看某个变量某个参数其值是如何一路赋值过来的。

##### 多行编辑

Alt+J

##### 列编辑

按住Alt加鼠标左键拉框即可

##### Enter和Tab在代码提示时的区别
比如现在我要向重新调用一个方法
enter：直接显示现在调用的方法，但是之前的方法依然存在需要手工删除
tab：替换之前的方法。

##### 选中指定的区域以及多块指定的区域

选中多块区域： shift + alt
选中指定区域： 鼠标点击指定区域的其实位置，按下 shift 在点击指定区域的结束位置

##### 在方法和内部类之间跳转

Alt + Up/Down (Windows/Linux)

##### 切换 tab 页

Ctrl + Tab（在 Android studio中的 tab 切换）

##### 弹出最常用的版本控制操作菜单

Alt + `(Windows/Linux)

##### 提取一段代码块，生成一个新的方法

Ctrl + Alt + M(Windows/Linux)

# Android studio 的插件安装

**一定要记得，如果插件是个压缩包一定要解压缩，操蛋我说怎么没有效果呢，原来是我没有解压，笑哭。**


### CodeGlance  
    
一个在右侧显示代码缩略图的插件很好用

### Sexy Editor

设置 code 编辑区的背景

# 编辑器字体设置

## 控制台字体设置

File -> Settings -> Editor -> Colors & Fonts -> Console Font

## 菜单项字体设置

File -> Settings -> Appearance & Behavior -> Appearance -> override default fonts by 

## 编辑框字体设置

File -> Settings -> Editor -> Colors & Fonts -> Font