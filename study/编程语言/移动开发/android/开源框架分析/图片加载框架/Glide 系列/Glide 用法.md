Glide是一款由Bump Technologies开发的图片加载框架.

项目地址： [戳我跳转](https://github.com/bumptech/glide)

#### 添加依赖

新建一个项目， 然后在 `app/build.gradle` 文件当中添加如下的依赖（注意：最新的依赖可以在项目主页上查看）：

```
dependencies {
    implementation 'com.github.bumptech.glide:glide:4.6.1'
    annotationProcessor 'com.github.bumptech.glide:compiler:4.6.1'
}
```

*注意一点， Glide 加载图片需要使用到网络功能， 所以还需要声明一下网络权限*

```
<uses-permission android:name="android.permission.INTERNET" />
```

#### 从一个 URL 中加载图片

```
ImageView targetImageView = (ImageView) findViewById(R.id.imageView);
String internetUrl = "http://i.imgur.com/DvpvklR.png";

Glide.with(context).load(internetUrl).into(targetImageView);
```

* `with(Context context)` - 对于很多 Android API 调用，[Context](http://developer.android.com/intl/zh-cn/reference/android/content/Context.html) 是必须的。Glide 在这里也一样
* `load(String imageUrl)` - 这里你可以指定哪个图片应该被加载，同上它会是一个字符串的形式表示一个网络图片的 URL
* `into(ImageView targetImageView)` 你的图片会显示到对应的 ImageView 中。

通过一行代码我们就可以看到图片了。

#### 从资源中加载

```
int resourceId = R.mipmap.ic_launcher;

Glide.with(context).load(resourceId).into(imageViewResource);
```

#### 从文件中加载

```
//这个文件可能不存在于你的设备中。然而你可以用任何文件路径，去指定一个图片路径。
File file = new File(Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES), "Running.jpg");

Glide.with(context).load(file).into(imageViewFile);
```

#### 问题

```
1. 无法使用 GlideAPP 问题
	在程序包名（不能在任何的二级包名）下，新建 Final类 继承AppGlideModule 
	例如我的：
		在程序包名下新建GlobalGlideConfig final类
			@GlideModule
            public final class GlobalGlideConfig extends AppGlideModule {}

```

