### 全屏

第一种

```
getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);
```

第二种（推荐）

```
在 style.xml 中新建一个主题

 <style name="FullScreenTheme" parent="AppTheme">
        <item name="android:windowFullscreen">true</item>
 </style>
 
 在 AndroidManifest.xml 中针对单个Activity分别设置主题
 
<activity
	android:name=".LauncherActivity" android:theme="@style/FullScreenTheme">
	<intent-filter>
		<action android:name="android.intent.action.MAIN" />
		<category android:name="android.intent.category.LAUNCHER" />
	</intent-filter>
</activity>
```

### 去掉标题栏

### 第一种：在oncreate方法中定义

```
//去掉标题栏注意这句一定要写在setContentView()方法的前面，不然会报错的
requestWindowFeature(Window.FEATURE_NO_TITLE);
```

### 第二种：在AndroidManifest.xml文件中定义

```
<application android:icon="@drawable/icon" 
        android:label="@string/app_name" 
        android:theme="@android:style/Theme.NoTitleBar">
```

可以看出，这样写的话，整个应用都会去掉标题栏，如果只想去掉某一个Activity的标题栏的话，可以把这个属性加到activity标签里面

### 第三种：

