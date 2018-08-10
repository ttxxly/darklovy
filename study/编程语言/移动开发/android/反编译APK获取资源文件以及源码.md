对 apk 反编译是必要的，我们今天介绍反编译工具，使用它们去获取 apk 的资源文件以及源代码。

### 所需工具：
* apktool（获取资源文件）  
* dex2jar（获取源码文件）
* jd-gui （查看源码）

[戳我 -- 下载工具](http://download.csdn.net/download/jdliyao/9825647)
### 工具用法

#### 1. 获取程序资源文件

1. 下载并解压 apktool 将需要反编译的APK文件放到该目录下。
2. 打开命令行界面（运行-CMD） ，定位到apktool文件夹，输入以下命令：

```
apktool.bat d -f  csdn.apk  csdn 
csdn 文件夹存放反编译之后得到的资源文件等

apktool.bat b test
将反编译之后的文件重新打包成 apk
```

#### 2. 获取源码

1. 下载并解压 dex2jar 和 d-gui
2. 将要反编译的APK后缀名改为.rar或.zip，并解压
3. 将其中的 classes.dex 放到之前解压出来的工具dex2jar-0.0.9.15 文件夹内
4. 在命令行下定位到 dex2jar.bat 所在目录，输入

```
dex2jar.bat classes.dex

在该目录下会生成一个 classes_dex2jar.jar 文件， 使用 jd-gui.exe 就可以打开这个文件查看源码了
```

#### 3. 使用 jadx 打开 apk 查看源码

1. 解压 jadx-0.6.1
2. 打开 双击 bin 目录下的 jadx-gui.bat 
3. 打开 apk 文件， 之后我们就可以查看的源码了