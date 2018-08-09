#### mysql 的安装和配置步骤

1. 下载链接：https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.21-winx64.zip

2. 将下载好的压缩包解压到 `D:\DataBase\mysql` 

3. 在 `D:\DataBase\mysql` 目录下创建 my.ini 文件。内容为:

   ```
   [mysql]  
   # 设置mysql客户端默认字符集  
   default-character-set=utf8  
   [mysqld]  
   #设置3306端口  
   port = 3306  
   # 设置mysql的安装目录  
   basedir=D:\DataBase\mysql
   # 设置mysql数据库的数据的存放目录  
   datadir=D:\DataBase\mysql\data  
   # 允许最大连接数  
   max_connections=200  
   # 服务端使用的字符集默认为8比特编码的latin1字符集  
   character-set-server=utf8  
   # 创建新表时将使用的默认存储引擎  
   default-storage-engine=INNODB  

   [WinMySQLAdmin]
   D:\DataBase\mysql\bin\mysqld.exe
   ```

4. 在 `D:\DataBase\mysql` 目录下创建 `data` 文件夹用于存放数据

5. 新建环境变量到 path 中

   ```
   D:\DataBase\mysql\bin
   ```

6. 安装 mysql **以管理员身份打开 cmd 窗口，将目录切换到mysql安装文件夹下的bin目录下 ** `目录：D:\DataBase\mysql\bin` 然后执行以下命令：

   ```
   mysqld -install
   ```

7. 初始化mysql数据库

   ```
   mysqld --initialize --user=root --console
   ```

   **注意：最后面的一串字符为初始化后的 root 密码**

8. 使用生成的密码登录mysql，通过“set password=password('123456')”修改密码。

   ```
   net start mysql
   mysql -uroot -p
   set password=password('123456');
   ```

#### mysql的卸载

1. 停止 mysql 服务

   ```
   win + R 打开运行窗口
   输入 services.msc 回车
   找到 mysql 将 mysql 服务停止
   ```

2. 卸载mysql server

   ```
   控制面板\所有控制面板项\卸载程序，将mysql server卸载掉。（没有找到就直接进行下一步）
   将MySQL安装目录下的MySQL文件夹删除（我的安装目录是 D:\DataBase\mysql）
   ```

3. 删除注册表

   ```
   Win + R 打开运行窗口
   输入 regedit 回车，打开注册表
   删除HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Eventlog\Application\MySQL文件夹
   删除HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\Eventlog\Application\MySQL文件夹。
   删除HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\MySQL的文件夹。
   如果没有相应的文件夹，就不用删除了。
   ```

4. 删除C盘下的 `C:\ProgramData\MySQL `  文件夹，无法删除就粉碎文件

   ```
   该programData文件默认是隐藏的，设置显示后即可见
   ```

5. 查看服务

   ```
   win + R 打开运行窗口
   输入 services.msc 回车
   如果仍然残留在系统服务里，就：
   	以管理员身份打开 cmd 窗口 输入 sc delete mysql 回车
   ```

6. 重启电脑


#### 常见的一些错误

```
1. 应用程序无法正常启动0xc000007b
	使用 百度云盘 工具包文件夹下的 DirectX Repair V3.5 压缩包
```

