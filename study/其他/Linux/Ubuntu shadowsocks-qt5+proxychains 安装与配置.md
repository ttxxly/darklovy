#### 第一部分：shadowsocks-qt5

````
https://github.com/shadowsocks/shadowsocks-qt5/releases

打开上面的网址，下载最新版。

然后自己新建连接。
````

#### 第二部分：proxychains

````
1. 安装
	sudo apt install proxychains
2. 配置
	sudo gedit /etc/proxychains.conf
	
	在文件的末尾
		#socks4 	127.0.0.1 9050	//注释这一行
		socks5 	127.0.0.1 1080		//再添加这一行
3. 测试
	proxychains curl www.google.com
	
	proxychains bash			//回车之后表示当前窗口所有的命令都会走代理
````

