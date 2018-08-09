### 免密码登录

1. 打开TortoiseGit下的PuttyGen，在打开的窗口中点击Generate按钮，会出现绿色进度条，等下生成，生成过程中可以多晃晃鼠标增加随机性。

2. 生成之后复制生成的全部内容在coding或者github上添加，窗口先留着不关闭。

3. 返回到第二步的窗口，点击Save private key按钮保存为适用于TortoiseGit的私钥扩展名为.ppk。

4. 运行TortoiseGit开始菜单中的Pageant程序，程序启动后将自动停靠在任务栏中，双击该图标，弹出key管理列表。

5. 在弹出的key管理列表中点击add key,将第4步中保存的私钥（.ppk）文件加进来，关闭对话框即可。
经上述配置后，就可以使用TortoiseGit进行push、pull操作了，不用每次都输入密码了。

### 解决git提交的时候总是提示key加载失败，总是需要手工将key加到Pageant中

ppk的保存路径和文件名都发生了变更，所以导致每次提交的时候，依据config都找不到ppk的地址，所以报错！

解决方法： 打开 TortoiseGit 设置 =》 Git =》 远端 =》 选中右侧的一个远端， 然后添加 Putty密钥 也就是本地的 *.ppk 文件。