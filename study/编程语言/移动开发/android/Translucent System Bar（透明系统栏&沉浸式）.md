从 Android 4.4 （API 19）开始，引入了 Translucent System Bar 这个特性（系统的通知栏和 APP 界面融为一体），用于弥补系统通知栏突兀之处。

首先我们需要了解一些界面的系统元素：

![](http://img.blog.csdn.net/20160820205313182)

而沉浸式的体验就是要将这些系统元素给全部隐藏，只留下主题内容部分。

#### 沉浸式模式

没有所谓的沉浸式状态栏，只有沉浸式模式，适用于游戏、视频类软件应用.

重写 Activity 的 onWindowFocusChanged() 方法即可。

```
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onWindowFocusChanged(boolean hasFocus) {
        super.onWindowFocusChanged(hasFocus);
        if (hasFocus && Build.VERSION.SDK_INT >= 19) {
            View decorView = getWindow().getDecorView();
            decorView.setSystemUiVisibility(
                View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
                | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN
                | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION
                | View.SYSTEM_UI_FLAG_FULLSCREEN
                | View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY);
        }
    }

}
```

实现效果：

![Translucent Mode](F:\pictures\网站用图\Translucent Mode.gif)

### 透明状态栏实现的两种方法

盗用两张图：

![](http://upload-images.jianshu.io/upload_images/912181-72351e6febce145c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/912181-683589389ba103a1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们注意看状态栏的位置，不再是系统默认的颜色了，对于整个界面来说不会在显得那么突兀了。

### 方法一：实现类似于中华万年历的效果，让图片占满状态栏

我们可以分为三个步骤来完成：

1. 对多个系统版本分别设置不同的主题
2. 修改指定 Activity 的主题
3. 在 XML 中设置背景图片

#### 1. 对多个系统版本分别设置不同的主题

* 调整代码呈现方式：由 Android 改为 Project
* 在 res 目录下 新建 **values-v19**、**values-v21** 文件夹
* 将**values** 目录下的 styles.xml 中 APPTheme 主题新增 `<item name="windowNoTitle">true</item>` 
* 再将 styles.xml 复制到 **values-v19**、**values-v21** 文件夹下
* 再然后分别对不同版本设置主题，如下。

values/style.xml 新增

```
<style name="ImageTranslucentTheme" parent="AppTheme">
	<!--在Android 4.4之前的版本上运行，直接跟随系统主题-->
</style>
```

values-v19/style.xml 新增

```
<style name="ImageTranslucentTheme" parent="AppTheme">
    <item name="android:windowTranslucentStatus">true</item>
    <item name="android:windowTranslucentNavigation">true</item>
</style>
```

values-v21/style.xml 新增

```
<style name="ImageTranslucentTheme" parent="AppTheme">
    <item name="android:windowTranslucentStatus">false</item>
    <item name="android:windowTranslucentNavigation">true</item>
    <!--Android 5.x开始需要把颜色设置透明，否则状态栏会呈现系统默认颜色-->
    <item name="android:statusBarColor">@android:color/transparent</item>
</style>
```

#### 2. 修改指定 Activity 的主题

在 AndroidManifest.xml 中：

```
<activity
    android:name=".ImageTranslucentBarActivity"
    android:theme="@style/ImageTranslucentTheme" />
```

#### 3.  设置 XML

在 activity_image_translucent_bar.xml 中设置背景和 `android:fitsSystemWindows="true"`

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="top.ttxxly.translucentsystembar.ImageTranslucentBarActivity"
    android:background="@mipmap/background"
    android:fitsSystemWindows="true">

</LinearLayout>

```

效果图：

![ImgStatusBar](F:\pictures\网站用图\ImgStatusBar.png)

### 实现 QQ 音乐类似效果

用的是另外一种实现的方式，它将app的Tab栏和系统状态栏分开来设置。

##### 参考

* http://blog.csdn.net/guolin_blog/article/details/51763825
* http://www.jianshu.com/p/0acc12c29c1b
* http://blog.csdn.net/u013260551/article/details/51150336
* http://blog.csdn.net/jdsjlzx/article/details/41643587