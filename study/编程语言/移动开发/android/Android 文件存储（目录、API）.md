 本篇文章将带领我们了解在Android中的文件存储。

```
这里主要介绍下面一些目录：
	内部存储中应用私有目录
	外部存储中应用私有目录
	外部存储中的共有目录
	外部存储中的其他目录
```

#### 内部存储中应用私有目录

```
Android中我们每安装一个APP都会在内部存储空间的 /data/data 目录下创建文件夹名字为应用包名的文件夹。

/data/data/包名/XXX 

用于存储一些配置、webView的缓存页面信息、SharedPreferences以及Database等数据。

常用的文件夹：
	1.data/data/包名/shared_prefs 存放该APP内的SP信息			
	2.data/data/包名/databases 存放该APP的数据库信息 
	3.data/data/包名/files 将APP的文件信息存放在files文件夹 
	4.data/data/包名/cache 存放的是APP的缓存信息 

常用的一些方法：
	位于 Application Context 中
		context.getFilesDir();
			获取内部存储中应用文件路径（/data/data/包名/Files）
				context.getFilesDir().getAbsolutePath()
				context.getFilesDir().getPath() 
		context.getCacheDir();
			获取内部存储中应用缓存路径（/data/data/包名/Cache）
				context.getCacheDir().getPath() 
		context.deleteFile();
		context.fileList();
	Environment 类
		Environment.getDataDirectory();
```

*当用户卸载APP时，系统会自动删除 `/data/data/APP对应包名` 文件夹及其内容*

#### 外部存储中应用私有目录

```
Android系统在外部存储空间中也提供特殊目录供应用存放私有文件。

文件路径：
	/storage/emulated/0/Android/data/app package name
常用方法：
	获取外部存储中应用文件路径
	context.getExternalFilesDir();
	context.getExternalCacheDir();
	Environment.getExternalStorageDirectory();
注意：
	1. 默认情况下系统不会自动创建外部存储的应用私有目录。
	2. 当前APP可以直接读写内部存储的应用私有目录
	3. 从4.4版本开始，当前APP才能直接读写外部存储的应用私有目录（低版本需要配置权限）。
	4. 同属于应用私有目录。在用户卸载APP时，也会删除外部存储中的应用私有目录和内容。
	5. 在外部存储的应用私有目录中，普通用户是可以自由的修改和删除文件，所以要做判空处理异常捕获。
```

#### 外部存储公共目录

```
持久化数据分类：
	应用相关数据：当前APP使用的数据信息（配置、缓存、数据库等，APP被卸载，数据就会被删除）
	应用无关数据：
		应用被卸载后，用户任然希望保留于设备当中的数据（拍照图片、视频、歌曲等）
		这些数据应该存放在外部存储空间的公共目录文件夹下。
外部存储中默认公共目录：
	Music
	Movies
	Pictures
	Download
	获取公共目录的方法：
		Environment.getExternalStoragePublicDirectory(String type);
		type参数可选：
			DIRECTORY_MUSIC：Music
			DIRECTORY_MOVIES：Movies
			DIRECTORY_PICTURES：Pictures
			DIRECTORY_DOWNLOADS：Download
注意：访问外部存储空间时记得申请读写权限！
```

#### 外部存储空间中的其他目录

```
一般来说，我们和数据和文件保存到私有目录和公共目录中，当然也可以保存到其他目录中，自由创建其他目录。

获取外部存储空间的绝对路径：
	Environment.getExternalStorageDirectory();
```

