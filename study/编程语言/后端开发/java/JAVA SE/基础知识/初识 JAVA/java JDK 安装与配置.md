JDK下载地址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

注意：

```
1. 电脑的系统版本X86（32位系统）、X86_X64（64系统）
2. 安装JDK的目录最好不要有中文目录，或者带有特殊符号的目录
```

双击安装包，选择安装安装JDK的目录即可开始安装。

##### 配置JDK的环境变量

```
系统环境变量：
	JAVA_HOME：JDK安装的根目录
	Path：%JAVA_HOME%\bin;
java -version:显示安装JDK的版本号，JDK的环境配置成功

JDK java开发套件  javac.exe
jre java的运行环境，没有编译源文件的执行程序（javac.exe）
```

##### 编写一个测试案例

```
编译：javac 源文件.java
执行：java 类名
```

1. 在 F:\projects\eclipse-workspace 目录下新建 `Hello.java`

```
public class Hello {
	public static void main(String[] args) {
		System.out.println("This is a java Application.");
	}
}
```

2. 打开控制台

```
C:\Users\ttxxl>F:
F:\>cd F:\projects\eclipse-workspace
F:\projects\eclipse-workspace>javac Hello.java
F:\projects\eclipse-workspace>java Hello
This is a java Application.
```

如果正常编译和执行Hello输出，代表JDK环境安装成功。



感兴趣的话可以点击下面的链接，关注我的微信公众号和我的知识星球。

> https://www.ttxxly.top/images/qrcode_darklovy.jpg
>
> https://www.ttxxly.top/images/qrcode_ttxxly123.jpg
>
> https://www.ttxxly.top/images/ZSXQ_darklovy.png



发表地址：

* https://blog.csdn.net/jdliyao/article/details/81198232
* [有道云笔记](http://note.youdao.com/noteshare?id=558356e88cbc7c210000a04dfa61b388&sub=55B94E552E554195A1DFB04B8429997F) 