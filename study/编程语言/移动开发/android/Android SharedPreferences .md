SharedPreferences 是 Android 平台上的一个轻量级存储类，主要保存一些常用的配置。

在 Android 系统中，这些信息以键值对的形式保存在 `data/data/包名/shared_prefs` 目录下的 xml 文件中。 

#### 用法

（1）使用Activity类的getSharedPreferences方法获得SharedPreferences对象，其中存储key-value的文件的名称由getSharedPreferences方法的第一个参数指定。

（2）使用SharedPreferences接口的edit获得SharedPreferences.Editor对象。

（3）通过SharedPreferences.Editor接口的putXxx方法保存key-value对。其中Xxx表示不同的数据类型。例如：字符串类型的value需要用putString方法。

（4）通过SharedPreferences.Editor接口的commit方法保存key-value对。commit方法相当于数据库事务中的提交（commit）操作。

#### 存放数据信息

```
//1、打开Preferences，名称为setting，如果存在则打开它，否则创建新的Preferences
SharedPreferences settings = getSharedPreferences("settings", 0);
//2、让setting处于编辑状态
SharedPreferences.Editor editor = settings.edit();
//3、存放数据
editor.putBoolean("is_guide_show", true);
//4、完成提交
editor.apply();
```

#### 读取数据信息

```
//1、获取Preferences
SharedPreferences settings = getSharedPreferences(“setting”, 0);
//2、取出数据
String name = settings.getString(“name”,”默认值”);
String url = setting.getString(“URL”,”default”);
//以上就是Android中SharedPreferences的使用方法，其中创建的Preferences文件存放位置可以在Eclipse中查看：
DDMS->File Explorer /<package name>/shared_prefs/setting.xml 
```

*注：setting 就是 xml 文件名* 







##### 参考

* http://blog.csdn.net/wxyyxc1992/article/details/17222841