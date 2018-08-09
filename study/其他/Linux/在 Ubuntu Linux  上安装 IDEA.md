#### 1. 下载

我们可以从JetBrains官方网站下载IntelliJ IDEA。

下载地址跳转：https://www.jetbrains.com/idea/download/#section=linux

#### 2. 安装

第一步是提取下载的压缩文件（放在你想要安装的位置）：

```
tar -zxvf ideaIC-2016.2.5.tar.gz
```

给脚本执行权限：

```
cd idea-IC-162.2228.15
sudo chmod a=+rx bin/idea.sh
bin/idea.sh
```

　注意：如果你想为所有用户安装IntelliJ IDEA，则必须使用超级用户权限执行脚本：

```
sudo bin/idea.sh
```

如果一切正常，则应出现安装窗口。

然后下一步就行。