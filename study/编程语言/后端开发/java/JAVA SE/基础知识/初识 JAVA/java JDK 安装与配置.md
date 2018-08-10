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



支持我的话可以关注下我的微信公众号，每天都会推送新知识~ 

> ![](C:\Users\ttxxl\Pictures\20180404220912740.jpg) ![](C:\Users\ttxxl\Pictures\qrcode_for_gh_e125acf2ab2b_258.jpg)

发表地址：

* https://blog.csdn.net/jdliyao/article/details/81198232
* https://mp.weixin.qq.com/s__biz=MzUxMTYyMjkxMg==&mid=2247483745&idx=1&sn=f809cf055af1895b3557e5931a8c7aa5&chksm=f971ab0ece062218e4cec9176b96b6374b4a997014e24d773d9bc3563caa5b86e816cee91cd4&mpshare=1&scene=1&srcid=0727xCXYHViaY2ZLAlRunsd2#rd