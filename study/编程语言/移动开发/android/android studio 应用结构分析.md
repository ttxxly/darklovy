* libs：存储 Android 项目所需的第三方JAR包。

* src：存放 Android 项目开发中的各种源文件，包括各种java源文件（main\java子目录下）、各种资源文件（main\res目录下）和 AndroidMainfest.xml 文件。还有一个 androidTest 子目录，该目录下存放的是 Android测试项目。

  AndroidMainfest.xml 文件是Android 项目的系统清单文件。它用于控制Android应用的名称、图标、访问权限等整体属性。初次之外，Android程序中的四大组件都需要在该文件中注册。

* res：存放 Android  项目的各种资源文件，比如 layout 存放界面文件， values 目录下存放各种xml格式的资源文件，比如字符串资源文件：string.xml ；颜色资源文件：colors.xml；尺寸资源文件：dimens.xml。drawable-ldpi、drawable-mdpi、drawable-hdpi、drawable-xhdpi 这4个子目录跟别存放低分辨率、中分辨率、高分辨率、超高分辨率的4种图片文件。