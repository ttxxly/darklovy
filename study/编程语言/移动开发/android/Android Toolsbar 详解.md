以一个常用的例子来讲解我们应该如何来使用 ToolBar，请看下图：

 ![toolbar](http://speed-up.cdn.ttxxly.top/toolbar.jpeg)

### 步骤

* 去掉系统自带的title
* 在 XML 中定义
* 设置标题、导航图标
* 添加菜单

### 去掉系统自带的title

在 styles.xml 中

```
 <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        <!-- 去掉标题栏 -->
        <item name="windowNoTitle">true</item>
    </style>
```

### 定义 ToolBar

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="top.ttxxly.appbarlayout.MainActivity">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar_main"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#336666">
    </android.support.v7.widget.Toolbar>

    <WebView
        android:id="@+id/wb_main"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

</LinearLayout>

```

定义ToolBar并设置背景颜色为 "#336666".

### 设置标题、图标等

在 MainActivity 中：

```
mToolbar.setTitle("Title");

//设置导航图标、添加菜单点击事件要在setSupportActionBar方法之后
setSupportActionBar(mToolbar);
mToolbar.setNavigationIcon(R.drawable.ic_web_delete);
```

### 添加菜单

```
@Override
public boolean onCreateOptionsMenu(Menu menu) {
	getMenuInflater().inflate(R.menu.menu_web, menu);
	return true;
}
```

### 设置点击事件

```
mToolbar.setOnMenuItemClickListener(new Toolbar.OnMenuItemClickListener() {
            @Override
            public boolean onMenuItemClick(MenuItem item) {
                switch (item.getItemId()) {
                    case R.id.web_refresh:
                        Toast.makeText(MainActivity.this, "你点击了刷新按钮！！", Toast.LENGTH_SHORT).show();
                        break;
                    case R.id.web_full_screen:
                        Toast.makeText(MainActivity.this, "全屏浏览", Toast.LENGTH_SHORT).show();
                        break;
                    case R.id.web_share:
                        Toast.makeText(MainActivity.this, "分享 !", Toast.LENGTH_SHORT).show();
                        break;
                    case R.id.web_copy:
                        Toast.makeText(MainActivity.this, "复制链接 !", Toast.LENGTH_SHORT).show();
                        break;
                    case R.id.web_launch:
                        Toast.makeText(MainActivity.this, "启动外部浏览器 !", Toast.LENGTH_SHORT).show();
                        break;
                    default:
                        break;
                }
                return true;
            }
        });
        mToolbar.setNavigationOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this, "关闭了页面", Toast.LENGTH_SHORT).show();
                finish();
            }
        });
```

有很多内容代码没有贴出来，如果有兴趣的话可以直接看源码。

源码地址：https://github.com/ttxxly/android/tree/master/AppBarLayout



#### 参考

* http://www.jianshu.com/p/ae0013a4f71a