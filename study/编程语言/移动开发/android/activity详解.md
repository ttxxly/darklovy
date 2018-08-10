activity是Android四大组件之一，其中所有的操作都与用户密切相关，是一个负责与用户交互的组件，可以通过 setContentView(View) 来显示组件。

### Activity整个生命周期的4种状态、7个重要方法

[官方文档](https://developer.android.com/reference/android/app/Activity.html)

![activity_lifecycle](http://okyfoew6j.bkt.clouddn.com/activity_lifecycle.png)

#### 4种基本状态

1. 活动（Active/Running）状态

当Activity运行在屏幕前台(处于当前任务活动栈的最上面),此时它获取了焦点能响应用户的操作,属于运行状态，同一个时刻只会有一个Activity 处于活动(Active)或运行

2. 暂停(Paused)状态

当Activity失去焦点但仍对用户可见(如在它之上有另一个透明的Activity或Toast、AlertDialog等弹出窗口时)它处于暂停状态。暂停的Activity仍然是存活状态(它保留着所有的状态和成员信息并保持和窗口管理器的连接),但是当系统内存极小时可以被系统杀掉

3. 停止(Stopped)状态

如果一个Activity被另外的Activity完全覆盖掉，叫做停止状态（Stopped）。它依然保持所有状态和成员信息，但是它不再可见，所以它的窗口被隐藏，当系统内存需要被用在其他地方的时候，Stopped的Activity将被强行终止掉。

4. 非活动（Dead）状态

如果一个Activity是Paused或者Stopped状态，系统可以将该Activity从内存中删除，Android系统采用两种方式进行删除，要么要求该Activity结束，要么直接终止它的进程。当该Activity再次显示给用户时，它必须重新开始和重置前面的状态。

#### 7个重要方法（建议看上图）

1. onCreate(Bundle savedInstanceState);

通常用于初始化(碎片和加载器)设置: 

* 使用setContentView加载布局
* 初始化控件和变量等
* 连接数据库并将数据绑定到list列表中

*注1：Activity还在后台，不可见（启动动画那些的还是不要来了吧）*  
*注2：这个方法会传递一个保存了此Activity上一状态信息的Bundle对象。紧随其后的方法总是onStart().*

2. onStart();

在此Activity可见（显示在前台）之前调用。
如果接着是显示在前台，紧随其后的方法是onResume()；如果接下来此Activity被隐藏了，则紧随其后的方法是onStop()。

3. onRestart()

处于停止态的Activity调用此方法，可以让此Activity重新显示在前台。
紧随其后的方法总是onStart()

4. onResume

Activity在这个阶段已经出现在前台并且可见了，可打开独占设备（相机等）此时该Activity位于Activity栈的顶部，在等待用户的操作（输入数据或点击按钮等）。紧随其后的方法是onPause().

5. onPause

当启动其他activity时调用此方法。在这个方法体里，通常用于提交未保存的数据、停止动画/视频和处理其他占用CPU资源的程序，等等。同时在这个方法体里处理的都是一些迅速快捷的操作，因为下一个activity会在onPause()方法执行完之后才可以在前台显示。
如果此Activity重新回到前台显示，则紧随其后的方法是onResume()；如果此Activity变得不可见了，则紧随其后的方法是onStop()

6. onStop()

当Activity不可见时调用此方法。这个方法的调用时刻是在Activity需要销毁或者被其他otherActivity取代且覆盖此Activity在前台显示时调用。
如果此Activity重新显示在前台，紧随其后的方法是onRestart()；如果此Activity需要被销毁，紧随其后的方法是onDestroy()

7. onDestroy

Activity被销毁时调用此方法。这是Activity生命周期里最后调用的一个方法。这个方法的调用可以发生在activity调用了finish()方法之后，或者是系统为了节省空间而销毁了此Activity的实例。你可以使用isFinishing()方法来区分这两种情况



### 创建一个Activity

编写一个继承 AppCompatActivity 的 Java 类并在 AndroidManifest.xml 声明即可。

1. 编写 java 类
```
public class MainActivity extends AppCompatActivity { 
    private static final String LOG_TAG = MainActivity.class.getSimpleName(); 
    @Override 
    public void onCreate(Bundle savedInstanceState) { 
        super.onCreate(savedInstanceState);      
        setContentView(R.layout.main); 
        Log.e(LOG_TAG, "onCreate"); 
    } 
   @Override 
    protected void onStart() { 
        Log.e(LOG_TAG, "onStart"); 
        super.onStart(); 
    } 
    @Override 
    protected void onResume() { 
        Log.e(LOG_TAG, "onResume"); 
        super.onResume(); 
    } 
    @Override 
    protected void onPause() { 
        Log.e(LOG_TAG, "onPause"); 
        super.onPause(); 
    } 
    @Override 
    protected void onStop() { 
        Log.e(LOG_TAG, "onStop"); 
        super.onStop(); 
    } 
    @Override 
    protected void onDestroy() { 
        Log.e(LOG_TAG, "onDestroy "); 
        super.onDestroy(); 
    } 
 }
```

2. 在 AndroidManifest.xml 声明

```
<activity android:name=".MainActivity" android:label="@string/app_name"> 
	 <intent-filter> 
		 <action android:name="android.intent.action.MAIN" /> 
		 <category android:name="android.intent.category.LAUNCHER" /> 
	 </intent-filter> 
 </activity>
```

### 在一个Activity启动另一个Activity    

```
 Intent intent =new Intent(CurrentActivity.this,OtherActivity.class); 
 startActivity(intent);
```

*注： 两个 Activity 都需要在 清单文件中配置*

### startActivityForResult

页面跳转之后，需要返回到之前的页面，同时要保留用户之前输入的信息.

步骤：
1. 从A页面跳转到B页面时，我们就不使用"startActivity()"方法了，使用"startActivityForResult"方法。
2. 在A页面的Activity中，需要重写"onActivityResult"方法

方法详解：

```
onActivityResult(int requestCode, int resultCode, Intent data)

第一个参数： 用于标识请求来源。
比如说： 一个Activity有两个按钮，点击这两个按钮都会打开同一个Activity
我想要知道新Activity是由那个按钮打开的。可以通过 requestCode 识别。

第二个参数：返回的数据来自于哪个新Activity

第三个参数：一个Intent对象，带有返回的数据。
```


### Activity 之间通信

#### 使用 Intent 通信

Android 中通过 Intent 对象来表示一条消息，一个 Intent 对象不仅包含有这个消息的目的地，还可以包含消息的内容，这好比一封 Email，其中不仅应该包含收件地址，还可以包含具体的内容。对于一个 Intent 对象，消息“目的地”是必须的，而内容则是可选项。

1. 发送信息，如果我们想要给“收件人”Activity 说点什么的话，那么可以通过下面这封“e-mail”来将我们消息传递出去：

```
Intent intent =new Intent(CurrentActivity.this,OtherActivity.class);
  // 创建一个带“收件人地址”的 email 
 Bundle bundle =new Bundle();// 创建 email 内容
 bundle.putBoolean("boolean_key", true);// 编写内容
 bundle.putString("string_key", "string_value"); 
 intent.putExtra("key", bundle);// 封装 email 
 startActivity(intent);// 启动新的 Activity
```

2. 接受信息，在 OtherActivity类的 onCreate()或者其它任何地方使用下面的代码就可以打开这封“e-mail”阅读其中的信息：

```
Intent intent =getIntent();// 收取 email 
 Bundle bundle =intent.getBundleExtra("key");// 打开 email 
 bundle.getBoolean("boolean_key");// 读取内容
 bundle.getString("string_key");
```

上面我们通过 bundle对象来传递信息，bundle维护了一个 HashMap< String, Object>对象，将我们的数据存贮在这个 HashMap 中来进行传递。但是像上面这样的代码稍显复杂，因为 Intent 内部为我们准备好了一个 bundle，所以我们也可以使用这种更为简便的方法：

```
Intent intent =new Intent(EX06.this,OtherActivity.class); 
intent.putExtra("boolean_key", true); 
intent.putExtra("string_key", "string_value"); 
startActivity(intent);
```

接收信息：

```
Intent intent=getIntent(); 
intent.getBooleanExtra("boolean_key",false); 
intent.getStringExtra("string_key");
```


#### 使用 SharedPreferences

SharedPreferences 使用 xml 格式为 Android 应用提供一种永久的数据存贮方式。对于一个 Android 应用，它存贮在文件系统的 /data/ data/your_app_package_name/shared_prefs/目录下，可以被处在同一个应用中的所有 Activity 访问

```
// 写入 SharedPreferences 
 SharedPreferences preferences = getSharedPreferences("name", MODE_PRIVATE); 
 Editor editor = preferences.edit(); 
 editor.putBoolean("boolean_key", true); 
 editor.putString("string_key", "string_value"); 
 editor.commit(); 
        
 // 读取 SharedPreferences 
 SharedPreferences preferences = getSharedPreferences("name", MODE_PRIVATE); 
 preferences.getBoolean("boolean_key", false); 
 preferences.getString("string_key", "default_value");
```

#### 其它方式

* SQLite
* 文件
* IPC方式


### 一些关于 Activity 的技巧

#### 锁定 Activity 运行时的屏幕方向

有时我们的应用程序仅能在横屏 / 竖屏时运行，比如某些游戏，此时我们需要锁定该 Activity 运行时的屏幕方向

< activity > 节点的 ``android:screenOrientation`` 属性 就是控制屏幕方向的。 

```
 <activity android:name=".MainActivity"
 android:label="@string/app_name" 
 android:screenOrientation="portrait">// 竖屏 , 值为 landscape 时为横屏
…………
 </activity>
```

#### 全屏

```
// 设置全屏模式
getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, 
WindowManager.LayoutParams.FLAG_FULLSCREEN); 
// 去除标题栏
requestWindowFeature(Window.FEATURE_NO_TITLE);
```

##### 参考：

* https://www.ibm.com/developerworks/cn/opensource/os-cn-android-actvt/
* http://blog.csdn.net/u011067360/article/details/24477307
* http://baike.baidu.com/item/Activity/7304419
* http://www.jianshu.com/p/fb44584daee3