#### Android 配置汇总

```
1. 配置JDK和SDK
2. 设置字体
	编辑域字体设置
	控制台字体设置
	侧边栏以及菜单字体设置
3. 添加api文档悬浮提示
4. 关闭大小写区分
5. 设置自动导包
6. 设置right margin警示线
7. 设置LogCat颜色
8. 自定义类注释
9. 修改配置
	修改 Gradle
	修改 .android 
10. 配置离线API文档
11. 常用插件汇总
12. Android Studio 使用小技巧
	自动提示忽略大小写
	全局查找/替换
	修改应用包名
13. 代码提示
```

#### 配置JDK和SDK

![](https://images2015.cnblogs.com/blog/641601/201608/641601-20160809223016293-1324408193.png)

上图中，选择“Project Structure”，弹出如下界面：（选择JDK和Android SDK的路径）

![img](https://images2015.cnblogs.com/blog/641601/201608/641601-20160809222759199-1573362003.png)

File-->Other Settings-->Default Sructure 也可修改。

#### 设置字体

选择菜单栏“File--settings--Editor--Colors&Fonts--Font”：

![img](https://images0.cnblogs.com/blog2015/641601/201505/072112034542723.png)

同样也可以修改控制台的字体：

![img](https://images0.cnblogs.com/blog2015/641601/201505/072113295172430.png)

修改完之后发现AS的一些默认字体如侧边栏的工程目录的字体并没有发生变化，如果想改的话，那还是改一下吧（我个人一般是不改的），修改AS的默认字体：

![img](https://images0.cnblogs.com/blog2015/641601/201505/072114237677589.png)

#### 添加api文档悬浮提示

AS默认是没有api文档悬浮提示的，只有按住【Ctrl+Q】太会出现提示。如果要添加api的自动悬浮提示，设置如下：

![img](https://images2015.cnblogs.com/blog/641601/201608/641601-20160810094650684-343880749.png)

上图中，在红框部分打钩就行了，不过这样做对电脑的性能消耗会增加，可以不设置，根据个人习惯。

#### 关闭大小写区分

AS默认的代码提示是**大小写敏感**的。那我想让AS对大小写不敏感，该怎么弄呢？操作如下：

![img](https://images2015.cnblogs.com/blog/641601/201608/641601-20160810095124793-871900743.png)

#### 设置自动导包

![img](https://images2015.cnblogs.com/blog/641601/201608/641601-20160810095451340-1973533860.png)

#### 设置right margin警示线

给代码编辑域设置一条竖线，这条线是用以提醒程序员，一行的代码长度最好不要超过这条线，可以如下设置： 
Settings –> Editor –> General -> Appearance ，勾选 Show right margin (configured in Code Style options) 。

![这里写图片描述](https://user-gold-cdn.xitu.io/2016/11/29/a45492ca99703daee5b40ac0043b7608?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

#### 设置LogCat颜色

最终效果

![这里写图片描述](https://user-gold-cdn.xitu.io/2016/11/29/df813f3868700e381231a873c066db01?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

1.在File->Settings中打开Android-Logcat

![这里写图片描述](https://user-gold-cdn.xitu.io/2016/11/29/7ce4250fdb26bf3cc3cf8879e609d907?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

2.按图中提示设置

![这里写图片描述](https://user-gold-cdn.xitu.io/2016/11/29/8a9ec440268a7708f41165f576c81fec?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

3.系统调色盘

![这里写图片描述](https://user-gold-cdn.xitu.io/2016/11/30/d677cff8e1d3af18fcb3dba48a3e5bcd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

下面是我使用的Log级别色值，仅供参考

```
VERBOSE：BBBBBB
DEBUG：0070BB
INFO：48BB31
WARN：BBBB23
ERROR：FF0006
ASSERT：8F0005
```

#### 自定义类注释

![img](https://images0.cnblogs.com/blog2015/641601/201505/072142107821807.png)

```
/**
 * description:
 *
 * @author  ${USER} 
 * @date ${YEAR}-${MONTH}-${DAY}
 * @mail author@gmail.com
 */

```

####  修改配置

##### `.gradle`文件夹的修改

这项比较简单，在Android Studio的配置选项中修改就行

![img](https://upload-images.jianshu.io/upload_images/48490-8642506f1d964ed1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

##### `.android`文件夹的修改

这个文件夹是由Android SDK配置模拟器生成的，也是最占空间的一个。
首先，需要添加一个系统的环境变量`ANDROID_SDK_HOME`，如下图：

![img](https://upload-images.jianshu.io/upload_images/48490-beb5b404f2274c43.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/493)

#### 配置离线API文档

```
https://blog.csdn.net/qq_28950007/article/details/50760904
```

#### 常用插件汇总

```
1. CodeGlance
2. GsonFormat

```

#### Android Studio 使用小技巧

```
1. 自动提示忽略大小写
2. 全局查找/替换
3. 修改应用包名
```

##### 自动提示忽略大小写

settings -> Code Completion 在第一项 Case sensitive completion 设置为 none

##### 全局查找/替换

```
全局查找：Edit ->Find ->Find in path
全局替换：Edit ->Find -> Replace in path
```

##### 修改应用包名

![](http://img.blog.csdn.net/20160615174836929)

修改包显示方式，方便修改包名。

- 选中所要修改包的节点
- 右键后选中：**Refactor -> Rename** （或者直接 shift + F6）
- 在弹窗里修改成想要的名字
- 再修改当前`Module`的`build.gradle`文件中的`applicationId`,改为跟你的包名一致；
- 修改当前`Module`的`AndroidManifest.xml`文件中的`manifest`节点里的`package`属性值，改为跟你的包名一致。
- 最后如果在android studio里面启用了代码混肴，记得要先关闭代码混肴。

#### 代码提示



发表于

```
https://blog.csdn.net/jdliyao/article/details/80111107
```

