这里介绍的是手动升级到你想要的版本。

```
1. 打开一个项目，
   在Studio中选择Project的视图
   找到目录gradle\wrapper\gradle-wrapper.properties这个文件
   直接看最后一行：
   	distributionUrl=https\://services.gradle.org/distributions/gradle-2.10-all.zip
   改成你想要的版本。
2. 修改Project下的build中的classpath
	classpath 'com.android.tools.build:gradle:2.1.0'
	注意1中Gradle版本和 2中Gradle插件版本要对应
3. 重启 Android Studio 
注意事项，我这是科学上网的情况， 如果不是那么还需要自己去下载对应的Gradle
```

![](https://upload-images.jianshu.io/upload_images/1638147-a1627dcbc5d6983e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

