Ubuntu 16.04 手动安装 Oracle JDK的步骤：

1. 去 Oracle 官网下载，[链接点此](http://www.oracle.com/technetwork/cn/java/javase/downloads/jdk8-downloads-2133151-zhs.html) 

2. 解压到当前目录下

   ```
   tar -zxvf jdk-8u111-linux-x64.tar.gz
   ```

3. 移动解压后的文件夹到自己想要放的位置

   ```
   mkdir /usr/lib/jdk
   mv jdk1.8.0_111  /usr/lib/jdk/jdk1.8
   ```

4. 设置环境变量

   ```
   方案一：
   	修改全局配置文件，作用于所有用户：
   		vim /etc/profile 
   	将下面的代码放在文件的末尾：
   　　　　export JAVA_HOME=/usr/lib/jdk/jdk1.8
   　　　　export JRE_HOME=${JAVA_HOME}/jre
   　　　　export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
   　　　　export PATH=.:${JAVA_HOME}/bin:$PATH
   　　　
   方案二：
   	修改当前用户配置文件，只作用于当前用户：
   		vim ~/.bashrc 
   	设置与上一样
   ```

5. 使我们修改的配置立刻生效

   ```
   source /etc/profile 
   或者 
   source ~/.bashrc
   ```

6. 检查是否安装成功

   ```
   java -version
   ```

   