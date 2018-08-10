## Intent 的定义

我们通过intent传入某种意图，而android就会根据这种意图，自动寻找合适的activity来启动，如果有多个条件符合的activity，就以列表的方式让用户手动选择一个。

## Intent 类型

* Explicit intents（显式）： 根据类名直接启动Activity、service等
* Implicit intents（隐式）： 声明一个通用的执行动作，系统从应用中找出匹配的（有多个的情况下，用户需要选择打开）

**注1： 在 android 5.0 以后， 启动一个服务必须是 Explicit intents**  

**注2： 隐式意图中接收意图的组件需要在Manifest中相应组件位置添加<inter-filer>.**

## Intent 属性

* Action
* Data
* Category
* Type
* Compent
* Extra

### Action

指的是 Intent 药执行的动作。是一个字符串常量。

常见的 Action：

```
ACTION_CALL activity 启动一个电话.
ACTION_EDIT activity 显示用户编辑的数据.
ACTION_MAIN activity 作为Task中第一个Activity启动
ACTION_SYNC activity 同步手机与数据服务器上的数据.
ACTION_BATTERY_LOW broadcast receiver 电池电量过低警告.
ACTION_HEADSET_PLUG broadcast receiver 插拔耳机警告
ACTION_SCREEN_ON broadcast receiver 屏幕变亮警告.
ACTION_TIMEZONE_CHANGED broadcast receiver 改变时区警告.
```

### Data

执行时要操作的数据。

在目标 `<data />` 标签中包含了以下几种子元素，他们定义了url的匹配规则：

* android:scheme    匹配url中的前缀，除了“http”、“https”、“tel”...之外，我们可以定义自己的前缀
* android:host      匹配url中的主机名部分，如“google.com”，如果定义为“*”则表示任意主机名
* android:port      匹配url中的端口
* android:path      匹配url中的路径

一个例子：

```
<activity android:name=".TargetActivity">  
<intent-filter>  
    <action android:name="com.scott.intent.action.TARGET"/>  
    <category android:name="android.intent.category.DEFAULT"/>  
    <data android:scheme="scott" android:host="com.scott.intent.data" android:port="7788" android:path="/target"/>  
</intent-filter>  
</activity>  
```


### Category

指定当前动作（Action）被执行的环境, 在指定的环境才能够被激活。

常见的 Category 属性：

```
CATEGORY_DEFAULT：Android系统中默认的执行方式.按照普通Activity的执行方式执行。表示所有intent都可以激活它　
CATEGORY_HOME：设置该组件为Home Activity。
CATEGORY_PREFERENCE：设置该组件为Preference。　
CATEGORY_LAUNCHER：设置该组件为在当前应用程序启动器中优先级最高的Activity.通常为入口ACTION_MAIN配合使用。
CATEGORY_BROWSABLE：设置该组件可以使用浏览器启动。表示该activity只能用来浏览网页。　
CATEGORY_GADGET：设置该组件可以内嵌到另外的Activity中。
```

**注： 如果该activity想要通过隐式intent方式激活，那么不能没有任何category设置，至少包含一个`android.intent.category.DEFAULT`**

### Type

Intent的Type属性显式指定Intent的数据类型（MIME）。一般Intent的数据类型能够根据数据本身进行判定，但是通过设置这个属性，可以强制采用显式指定的类型而不再进行推导

### Compent

Intent的Compent属性指定Intent的的目标组件的类名称。通常 Android会根据Intent 中包含的其它属性的信息，比如action、data/type、category进行查找，最终找到一个与之匹配的目标组件。但是，如果 component这个属性有指定的话，将直接使用它指定的组件，而不再执行上述查找过程。指定了这个属性以后，Intent的其它所有属性都是可选的。

### Extra

Intent的Extra属性是添加一些组件的附加信息。比如，如果我们要通过一个Activity来发送一个Email，就可以通过Extra属性来添加subject和body。


## Intent 调用常见系统组件方法

```
// 调用浏览器  
Uri webViewUri = Uri.parse("http://blog.csdn.net/zuolongsnail");  
Intent intent = new Intent(Intent.ACTION_VIEW, webViewUri);  
  
// 调用地图  
Uri mapUri = Uri.parse("geo:100,100");  
Intent intent = new Intent(Intent.ACTION_VIEW, mapUri);  
  
// 播放mp3  
Uri playUri = Uri.parse("file:///sdcard/test.mp3");  
Intent intent = new Intent(Intent.ACTION_VIEW, playUri);  
intent.setDataAndType(playUri, "audio/mp3");  
  
// 调用拨打电话  
Uri dialUri = Uri.parse("tel:10086");  
Intent intent = new Intent(Intent.ACTION_DIAL, dialUri);  
// 直接拨打电话，需要加上权限<uses-permission id="android.permission.CALL_PHONE" />  
Uri callUri = Uri.parse("tel:10086");  
Intent intent = new Intent(Intent.ACTION_CALL, callUri);  
  
// 调用发邮件（这里要事先配置好的系统Email，否则是调不出发邮件界面的）  
Uri emailUri = Uri.parse("mailto:zuolongsnail@163.com");  
Intent intent = new Intent(Intent.ACTION_SENDTO, emailUri);  
// 直接发邮件  
Intent intent = new Intent(Intent.ACTION_SEND);  
String[] tos = { "zuolongsnail@gmail.com" };  
String[] ccs = { "zuolongsnail@163.com" };  
intent.putExtra(Intent.EXTRA_EMAIL, tos);  
intent.putExtra(Intent.EXTRA_CC, ccs);  
intent.putExtra(Intent.EXTRA_TEXT, "the email text");  
intent.putExtra(Intent.EXTRA_SUBJECT, "subject");  
intent.setType("text/plain");  
Intent.createChooser(intent, "Choose Email Client");  
  
// 发短信  
Intent intent = new Intent(Intent.ACTION_VIEW);  
intent.putExtra("sms_body", "the sms text");  
intent.setType("vnd.android-dir/mms-sms");  
// 直接发短信  
Uri smsToUri = Uri.parse("smsto:10086");  
Intent intent = new Intent(Intent.ACTION_SENDTO, smsToUri);  
intent.putExtra("sms_body", "the sms text");  
// 发彩信  
Uri mmsUri = Uri.parse("content://media/external/images/media/23");  
Intent intent = new Intent(Intent.ACTION_SEND);  
intent.putExtra("sms_body", "the sms text");  
intent.putExtra(Intent.EXTRA_STREAM, mmsUri);  
intent.setType("image/png");  
  
// 卸载应用  
Uri uninstallUri = Uri.fromParts("package", "com.app.test", null);  
Intent intent = new Intent(Intent.ACTION_DELETE, uninstallUri);  
// 安装应用  
Intent intent = new Intent(Intent.ACTION_VIEW);  
intent.setDataAndType(Uri.fromFile(new File("/sdcard/test.apk"), "application/vnd.android.package-archive");  
  
// 在Android Market中查找应用  
Uri uri = Uri.parse("market://search?q=愤怒的小鸟");           
Intent intent = new Intent(Intent.ACTION_VIEW, uri);  
```
### 参考

* http://www.jianshu.com/p/abd5eac1a02e