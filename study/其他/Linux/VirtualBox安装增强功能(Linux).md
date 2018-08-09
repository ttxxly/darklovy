一、安装依赖包

```c++
yum install kernel-headers
yum install kernel-devel
yum install gcc*    
yum install make
```

二、安装增强功能包

1、安装命令

```
mount /dev/cdrom /mnt/cdrom   
cd /mnt/cdrom
./VBoxLinuxAdditions.run
```
这里安装的时候可能要等上一会，大家耐心点哦！安装完成后，一般都要重启

2、 共享设置

(1) 设备->分配数据空间

(2) 挂载/卸载命令

```
mkdir /mnt/share
mount -t vboxsf myshare /mnt/share/      
umount -f /mnt/share
```
(3)开机自动共享

```
vim /etc/fstab
```

添加一项

``` 
myshare /mnt/share vboxsf rw,gid=100,uid=1000,auto 0 0
```