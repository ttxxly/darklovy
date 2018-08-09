官网：<http://www.sublimetext.com/3>

Sublime Text的特色功能：

- 良好的扩展功能，官方称之为安装包(Package)。
- 右边没有滚动条，取而代之的是代码缩略图，这个功能非常赞
- 强大的快捷命令“可以实时搜索到相应的命令、选项、snippet 和 syntex， 按下回车就可以直接执行，减少了查找的麻烦。”
- 即时的文件切换。
- 随心所欲的跳转到任意文件的任意位置。
- 多重选择(Multi-Selection)功能允许在页面中同时存在多个光标。
- 支持 VIM 模式
- 支持宏，简单地说就是把操作录制下来或者自己编写命令，然后播放刚才录制的操作或者命令。
- 更新非常勤快

 #### 安装教程

打开终端，输入以下命令： 

```
sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-get update
sudo apt-get install sublime-text-installer
```

卸载 sublime text 命令：

```
sudo apt-get remove sublime-text-installer
```

  当然也可以从官网直接下载.deb包并双击安装 http://www.sublimetext.com/3

#### 安装包管理器

按`ctrl+·`访问，将如下代码复制到控制台

注意：建议从官方源复制，下面的代码来自

https://packagecontrol.io/installation#st3

```
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

