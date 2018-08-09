需要注意的地方

```
/etc/apt/sources.list 文件
/etc/apt/sources.list.d 目录
```

##### sources.list 文件

```
里面保存的是官方的软件源，你可以任一选择阿里、网易等国内的源复制粘贴进去，保存。

然后更新源
sudo apt-get update
```

##### sources.list.d 目录

```
该文件夹下的文件是第三方软件的源，可以分别存放不同的第三源地址，只需“扩展名”为list即可

修改之后，同样需要更新一下源

sudo apt-get update
```





