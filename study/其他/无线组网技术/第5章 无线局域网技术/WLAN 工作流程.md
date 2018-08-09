### WLAN工作流程

 ![WLAN工作流程](F:\pictures\网站用图\WLAN工作流程.png)

### 瘦AP发现和会话建立流程

1. AP接入交换机端口。AP加电并获得IP地址（主要通过HDCP方式）
2. AP 查找 AC地址
3. AP从AC下载 image 文件（TFTP）并建立隧道连接到AC
4. AP认证后建立AP到交换机之间的隧道连接
5. 隧道建立完成后，AP从AC下载相应的配置文件完成自身配置。
6. WLAN用户终端与AP通信，AP将业务数据通过隧道传送到AC，由AC集中转发/也可设置成AP本地转发。