文件读写是非常常见的操作，按照一定的步骤即可实现文件读写操作。

#### 文件读写步骤

```
1. 配置读写权限
2. 判断SK卡是否存在（现在一般是内置ROM）
3. 获取SK卡根目录
4. 获取默认的文件存放路径
5. 使用 FileInputStream 读取文件

```



读写权限：

```
<!-- SDCard中创建与删除文件权限 -->  
  <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>  
 <!-- 向SDCard写入数据权限 -->  
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/> 
```

