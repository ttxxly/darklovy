# Vultr VPS搭建SS教程

> 本系列文章自由转载，注明原文地址即可。

### 国外服务器的购买

这里我选择的是Vultr，对比了很多国外的服务器，这个蛮靠谱的，且搭建成功后看youtube1080p完全无压力。

这里是链接：[Vultr The Infrastructure Cloud™](https://link.jianshu.com/?t=https%3A%2F%2Fwww.vultr.com%2F%3Fref%3D7295935)

当然，已经有服务器的小伙伴，直接从==快速搭建ShadowSocks==开始看

#### Vultr服务器价格

Vultr服务器按小时计费,最低0.004美元/h,算起来2.5美元/月，且destory掉服务器是不收费的，所以不用担心如果暂时没有使用还一直扣费的问题，如下图所示：

![img](https://upload-images.jianshu.io/upload_images/3883542-5a37a53b4fb0aacb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

最低价格的服务器是512M的内存，500G的带宽，只能说99%的情况下完全够用了！

#### 注册Vultr

首先打开[Vultr链接](https://link.jianshu.com/?t=https%3A%2F%2Fwww.vultr.com%2F%3Fref%3D7295935)，点击Create Account

#### 充值Vultr

#### ![img](https://upload-images.jianshu.io/upload_images/3883542-a393d98c540c2923.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

注册完成之后就是充值，Vultr提供4种充值方式，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-2b240230b4a8c30a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

这里我选择支付宝，因为方便快捷，但是最低消费10美元，也不多，60多人民币，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-49cc09a7e6e55d3a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

付款之后，就可以看到账户的钱多了

#### 选择VPS的位置

首先，位置很重要！我们如何选择呢，当然有科学的办法，ping它！

Vultr的服务器有很多位置，下面我测试的东京节点和新加坡节点的数据如下：

![img](https://upload-images.jianshu.io/upload_images/3883542-7192d20013fdb116.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

![img](https://upload-images.jianshu.io/upload_images/3883542-685cbb5130cd6a27.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

这么看来还是东京的节点速度比较好，当然这个因人而异，在中国不同的地理位置访问国外不同位置的服务器速度也不一样。（下面提供了下载地址,下载下来双击运行即可）。

测速脚本下载地址：
[点我下载 测速.bat](https://link.jianshu.com/?t=http%3A%2F%2Fp1hy9syru.bkt.clouddn.com%2F%25E6%25B5%258B%25E9%2580%259F.bat)

脚本内容如下：

```
@echo off
echo ===========================================
echo 东京
ping hnd-jp-ping.vultr.com

echo ============================================
echo 新加坡
ping sgp-ping.vultr.com

echo ===========================================
echo (AU) Sydney, Australia[悉尼]
ping syd-au-ping.vultr.com

echo ===========================================
echo 德国 法兰克福
ping fra-de-ping.vultr.com

echo ===========================================
echo 荷兰 阿姆斯特丹
ping ams-nl-ping.vultr.com

echo ===========================================
echo 英国 伦敦
ping lon-gb-ping.vultr.com

echo ===========================================
echo 法国 巴黎
ping par-fr-ping.vultr.com

echo ===========================================
echo 美东 华盛顿州 西雅图
ping wa-us-ping.vultr.com

echo ===========================================
echo 美西 加州 硅谷
ping sjo-ca-us-ping.vultr.com

echo ===========================================
echo 美西 加州 洛杉矶
ping lax-ca-us-ping.vultr.com

echo ===========================================
echo 美东 芝加哥
Chicago, Illinois[美东 芝加哥]
ping il-us-ping.vultr.com

echo ===========================================
echo 美中 德克萨斯州 达拉斯
ping tx-us-ping.vultr.com

echo ===========================================
echo 美东 新泽西
ping nj-us-ping.vultr.com

echo ===========================================
echo 美东 乔治亚州 亚特兰大
ping ga-us-ping.vultr.com

echo ===========================================
echo 美东 佛罗里达州 迈阿密
ping fl-us-ping.vultr.com   
pause
```

根据测速的结果，我选择东京位置的VPS

#### 创建VPS

左侧菜单栏Servers，点击+，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-ee1d05af94ce2141.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

选择VPS的位置，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-eab85cb6568d8de9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

选择操作系统和价格，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-03fb9399994d0fed.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

点击最下面的Deploy Now，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-32fe2a620e144c34.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

创建成功

![img](https://upload-images.jianshu.io/upload_images/3883542-9ccd708aa1da7171.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

#### VPS的信息

安装成功之后，点击Manage

![img](https://upload-images.jianshu.io/upload_images/3883542-8dc96ccd0c6d8ead.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

[图片上传中...(image-d6ecb2-1514626664095)]

可以看到你购买的VPS的信息，如下图所示：

![img](https://upload-images.jianshu.io/upload_images/3883542-094f80d577b336b3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

ping一下ip地址，100ms多一点，这个速度相当可以了，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-6dcffcba340bfed9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

### VPS的使用

#### 下载Shell

当然是选择先连接它了，我们选择的工具是XShell

下载地址：[Xshell下载](https://link.jianshu.com/?t=http%3A%2F%2Fp1hy9syru.bkt.clouddn.com%2FXshell5.zip)

下载完成之后安装，下一步即可

![img](https://upload-images.jianshu.io/upload_images/3883542-efd55f89d73a3a4e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/624)

image

接着选择免费为家庭/学校

![img](https://upload-images.jianshu.io/upload_images/3883542-d152b4a16ce5395f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/624)

image

语言选择中文：

![img](https://upload-images.jianshu.io/upload_images/3883542-7732828642a07ccf.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/624)

image

安装成功后打开

#### 连接VPS

打开Xshell，选择文件->新建，输入VPS的IP，IP地址就在Vultr的管理页面上，如下图所示：

![img](https://upload-images.jianshu.io/upload_images/3883542-e9aab3ea6cd1a961.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/667)

点击确定，输入用户名，默认应该为root，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-59a57a713d8295e3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/398)

image

接着输入密码：

![img](https://upload-images.jianshu.io/upload_images/3883542-7f5bb802df979df0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/504)

image

连接成功：

![img](https://upload-images.jianshu.io/upload_images/3883542-1e4faf8294542487.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

### 快速搭建ShadowSocks(二选一)

#### 一键安装

##### 使用方法

在Xshell中依次运行以下命令

```
wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh

chmod +x shadowsocks.sh

./shadowsocks.sh 2>&1 | tee shadowsocks.log
```

接着按照提醒输入你的密码，端口和加密方式，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-74a7d62e2e94d543.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

![img](https://upload-images.jianshu.io/upload_images/3883542-fa86ce3db77be186.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

然后可以去听首歌~，成功安装之后有你配置的信息显示，记住这些信息，然后跳过下面的手动安装部分，直接去看客户端连接部分即可，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-199ab70c25fde457.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/568)

image

> 以上脚本来源于秋水逸冰

#### 手动安装

##### 安装依赖包

在XShell的控制台输入：

```
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
```

一个个的来，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-9de77734fd2714b1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

##### 安装ShadowSocks

```
pip install --upgrade pip
pip install shadowsocks
```

如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-332ba1a059cbd935.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

##### 创建ShadowSocks配置文件

###### 单端口

```
vi /etc/shadowsocks.json
```

输入以下内容，然后点ESC后输入:wq保存退出

```
{
  "server": "0.0.0.0",
  "server_port": 2018,
  "password": "12345678",
  "method": "aes-256-cfb"
}
```

###### 多端口

（可选，配置了单端口就不要配置这个）多端口的配置文件如下：

```
{
    "server": "0.0.0.0",
    "port_password": {
        "8381": "password1",
        "8382": "password2",
        "8383": "password3",
        "8384": "password4"
    },
    "timeout": 300,
    "method": "aes-256-cfb"
}
```

我采取的是单端口配置，如下图所示：

![img](https://upload-images.jianshu.io/upload_images/3883542-56854846c8968c5a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

![img](https://upload-images.jianshu.io/upload_images/3883542-cb48bdd4f6ec44ea.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

##### 配置防火墙

```
systemctl stop firewalld.service
```

![img](https://upload-images.jianshu.io/upload_images/3883542-b59307a636a059b2.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/457)

image

##### 启动ShadowSocks服务

```
ssserver -c /etc/shadowsocks.json -d start
```

如图所示：

![img](https://upload-images.jianshu.io/upload_images/3883542-06dd9301c164b087.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/650)

image

下面的是关闭，启动成功之后不要执行

##### 关闭ShadowSocks服务

```
ssserver -c /etc/shadowsocks.json -d stop 
```

### 连接ShadowSocks，体会科学上网的魅力

#### Windows客户端

下载地址：
[Shadowsocks-4.0.7.zip](https://link.jianshu.com/?t=http%3A%2F%2Fp1hy9syru.bkt.clouddn.com%2FShadowsocks-4.0.7.zip)

下载完成之后解压打开，如下图所示：

![img](https://upload-images.jianshu.io/upload_images/3883542-b4f235178abfb563.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/578)

image

按照你自己的配置完成之后，点击确定，然后在托盘中右键这个小飞机，启动系统代理
，灰色的小飞机就会亮起来，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-e77cc63c73aa05dd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/324)

image

然后就可以畅游网络了~

测试地址：

- [谷歌](https://link.jianshu.com/?t=https%3A%2F%2Fwww.google.com.hk%2F)
- [Youtube](https://link.jianshu.com/?t=https%3A%2F%2Fwww.youtube.com%2F)
- [推特](https://link.jianshu.com/?t=https%3A%2F%2Ftwitter.com%2F%3Flang%3Dzh-cn)

#### 安卓连接

下载地址：[shadowsocks.apk](https://link.jianshu.com/?t=http%3A%2F%2Fp1hy9syru.bkt.clouddn.com%2Fshadowsocks.apk)

配置和windows差不多，配置完成后点击右上角的开启按钮即可，如下图：

![img](https://upload-images.jianshu.io/upload_images/3883542-f59bade6d27f4fdc.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/473)

image

#### IOS连接

参考链接：[http://www.360doc.com/content/17/0614/06/37032448_662846097.shtml](https://link.jianshu.com/?t=http%3A%2F%2Fwww.360doc.com%2Fcontent%2F17%2F0614%2F06%2F37032448_662846097.shtml)

#### MAC 连接

下载地址：
[ShadowsocksX-2.6.3.dmg](https://link.jianshu.com/?t=http%3A%2F%2Fp1hy9syru.bkt.clouddn.com%2FShadowsocksX-2.6.3.dmg)

### 测试结果

4K Youtube完成无压力

 

![img](https://upload-images.jianshu.io/upload_images/3883542-93f23f123f91768f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

image

### 写在后面的话

搭建完成后推荐看这篇文章，完成对网速的优化：[VPS搭建BBR加速教程（youtube1440p无压力）](https://link.jianshu.com/?t=http%3A%2F%2Fwww.hellojava.club%2Farticle%2F5)

如果想多利用[Vultr](https://link.jianshu.com/?t=https%3A%2F%2Fwww.vultr.com%2F%3Fref%3D7295935)，搭建个人博客，看这篇文章：[10分钟搭建Java开源博客Tale-超详细](https://link.jianshu.com/?t=http%3A%2F%2Fwww.hellojava.club%2Farticle%2F7)

本文转载自：https://www.jianshu.com/p/1c82ee1293a4?open_source=weibo_search