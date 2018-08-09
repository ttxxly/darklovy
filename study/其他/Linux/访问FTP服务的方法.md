## 访问FTP服务的方法

(1)资源管理器

(2) 命令行

* cmd命令，打开命令行
* ftp ftp.cs.nsu.edu.cn

(3)Web浏览器

* ftp://ftp.cs.nsu.edu.cn
    
(4)第三方FTP客户端工具
    
* cuteFtp(Windows)
* filezilla(win, linux )

## ftp服务工作原理

### 工作模式

(1) 主动模式

* 控制连接21端口
* 数据连接20端口

(2) 被动模式

* 控制连接21端口
* 数据连接大于1024的任意一个端口（由客户端发送的一个端口号）
    
## ftp传输文件方式
    
* ASCII码(American Standard Code For Information Interchange)

文本文件

* 二进制

