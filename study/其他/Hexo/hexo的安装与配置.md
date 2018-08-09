```
安装流程：
	1. 安装Node.js
	2. 安装Git → 安装Hexo
	3. 安装主题 
	4. 本地测试运行
	5. 在github与coding上创建pages仓库
	6. 部署到远程仓库中
	7. 自定义域名访问
配置与优化
	1. 添加标签页面
	2. 添加分类页面
	3. 添加自定义页面
	4. 文章末尾追加版权信息
	5. 开启打赏功能
	6. 友情链接
	7. 自定义字体
	8. 自定义图标和侧栏头像
	9. 添加 Rss 订阅
	10. MathJax支持
错误解决
	1. 关于网站图标不更新问题
```

#### 安装 Hexo

##### Node.js、GIt 安装

* 参考 https://hexo.io/zh-cn/docs/index.html
##### 安装hexo

打开 `git bash` 输入以下命令

```
npm install -g hexo-cli
```

安装 `Hexo` 完成后，请执行下列命令，请特别的注意看注释。

```
hexo init <folder>  #folder指我们要安装的博客根目录 
				  #hexo init blog 指的是在当前文件夹下新建blog目录作为博客的根目录
cd <folder>
npm install         #安装所有的依赖包
```

##### 安装主题

* 将主题文件拷贝至站点目录的 ``themes`` 目录下

```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

* 修改配置文件  
  打开 **站点配置文件**， Ctrl +F 搜索 ``theme`` 字段，并将其值更改为 next  
  如果显示的是繁体中文，那么在**站点配置文件**中设置 `language: zh-CN`

* 本地预览

  ```shell
  hexo g # 等同于hexo generate，生成静态文件
  hexo s # 等同于hexo server，在本地服务器运行
  ```

* 打开浏览器输入 http://localhost:4000  能够访问说明部署成功。

##### 注册 Github 并创建Pages

1. 在 https://github.com/ 上面注册一个账号

2. 新建仓库，仓库名为`你账号用户名.github.io`

3. 设置 SSH 远程连接

   * 设置Git的user name和email：(如果是第一次的话)

   ```
   git config --global user.name "ttxxly"
   git config --global user.email "ttxxly@gmail.com"
   ```

   * 生成密钥

   ```
   ssh-keygen -t rsa -C "ttxxly@gmail.com"
   ```

   连续3个回车。如果不需要密码的话。
   最后得到了两个文件：`id_rsa`和`id_rsa.pub`。复制 `id_rsa.pub`内容到github上。

##### 部署到 github

在 博客的配置文件（不是主题配置文件） `_config.yml` 中 末尾添加

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo:
    github: git@github.com:ttxxly/ttxxly.github.io.git,master
    coding: git@git.coding.net:ttxxly/ttxxly.coding.me.git,master
```

再然后打开 `Git bash` 输入 `hexo d` 就是可以提交内容到GitHub上，然后就可以通过仓库名 `ttxxly.github.io` 来访问。

*注意一个公钥只能配置在一个网站，放在github就不能再放在 coding上*

##### 自定义域名访问

1. 在 `blog\source`目录下新建 `CNAME`文件

```
#### 在 CNAME 文件 中 填写自定义域名, 格式如下
ttxxly.top
```

#### 配置与优化

##### 添加标签页面

```
/*
必看！！！！
	确认站点配置文件_config.yml中有： tag_dir： tags （有注释的去掉注释）
	确认主题配置文件_config.yml中有： tags: /tags
*/
hexo new page "tags"
```

编辑站点中 ``source/tags/index.md`` 文件：

```
title: tags
date: 2017-3-16 14:08:51
type: "tags"
```

如果站点启用多说或者Disqus，会在默认页面添加评论，关闭评论那么还需要添加:

```
comments： false
```

##### 添加分类页面

```
/*
确认站点配置文件里有 category_dir: categories
确认主题配置文件里有 categories: /categories
*/
hexo new page "categories"
```

编辑站点的 ``source/categories/index.md`` 文件：

```
title: categories
date: 2015-10-20 06:49:50
type: "categories"
```

如果站点启用多说或者Disqus，会在默认页面添加评论，关闭评论那么还需要添加:

```
comments： false
```

##### 添加自定义页面

```
hexo new page "title"
```

* 如果你不想在该页面显示评论，那么我们需要打开 ``blog\source\logs\index.md`` 在date的 **下一行**添加 ``comments: false``(注意冒号后面有一个空格)
* 找到 ``\next\_config.yml`` 下的 ``menu`` ， 把 ``title`` 加进去。
* 然后在下面 ``menu_icons`` 中加入你想让其显示的图标[图标传送](http://fontawesome.io/icons/)
* 在 ``/themes/hexo-theme-next/languages/zh-Hans.yml`` 文件中（这里默认你使用的是简体中文，若是其他语言更改相应的yml就行），在 ``memu`` 下加一句即可：

```
title: 标题
```

##### 文章末尾追加版权信息

打开 `themes/next/layout/_macro/reward.swig` ，在最上面添加如下代码：


```
<div align="center">
 {% if not is_index %}
   <div class="">
   <p>
    <span>
      <b>本文地址：</b>
      <a href="{{ url_for(page.path) }}" title="{{ page.title }}">{{ url_for(page.path) }}</a>
      <br/><b>转载请注明出处，谢谢！</b>
    </span>
   </p>
   </div>
 {% endif %}
</div>
```

##### 开启打赏功能

在 `主题配置文件` 中：

```
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /images/wechat-reward.png
alipay: /images/alipay-reward.jpg
```

##### 友情链接

在 `主题配置文件` 中

实例：

```
# title
links_title: Links
links:
  MacTalk: http://macshuo.com/
  Title: http://example.com/
```

##### 自定义字体

[http://theme-next.iissnan.com/theme-settings.html#fonts-customization](http://theme-next.iissnan.com/theme-settings.html#fonts-customization)

```
font:
  enable: true

  # 外链字体库地址，例如 //fonts.googleapis.com (默认值)
  host:

  # 全局字体，应用在 body 元素上
  global:
    external: true
    family: Monda

  # 标题字体 (h1, h2, h3, h4, h5, h6)
  headings:
    external: true
    family: Roboto Slab

  # 文章字体
  posts:
    external: true
    family:

  # Logo 字体
  logo:
    external: true
    family: Lobster Two
    size: 24

  # 代码字体，应用于 code 以及代码块
  codes:
    external: true
    family: PT Mono
```

[官方文档：自定义字体](http://theme-next.iissnan.com/faqs.html#custom-font "官方文档：自定义字体")

在 `source/css/_variables/custom.styl` 文件中

```
// 标题，修改成你期望的字体族
$font-family-headings = Georgia, sans

// 修改成你期望的字体族 如果不生效 请在同目录下的 base.style 下 修改成你期望的字体族
$font-family-base = "Microsoft YaHei", Verdana, sans-serif

// 代码字体
$code-font-family = "Input Mono", "PT Mono", Consolas, Monaco, Menlo, monospace

// 正文字体的大小
$font-size-base = 16px

// 代码字体的大小
$code-font-size = 13px
```

*注：上面的那种方式是更改首选字体，下面的方式会覆盖上面的那一种方式*

##### 自定义图标和侧栏头像

图标：在 ``source`` 目录下，放图标文件，命名为 ``favicon.ico``
侧栏头像： 编辑 **站点配置文件** `` _config.yml`` ，新增字段 ``avatar``，值设置成头像的链接地址。

```
其中，头像的链接地址可以是：

完整的互联网 URL，例如：https://avatars1.githubusercontent.com/u/32269?v=3&s=460
站点内的地址，例如：

/uploads/avatar.jpg 需要将你的头像图片放置在 站点的 source/uploads/（可能需要新建uploads目录）
/images/avatar.jpg 需要将你的头像图片放置在 主题的 source/images/ 目录下。
```

##### 添加RSS订阅

安装订阅插件：

```
npm install hexo-generator-feed

```
编辑网站根目录下的 _config.yml，添加以下代码开启

```
# RSS订阅支持
plugin:
- hexo-generator-feed

# Feed Atom
feed:
type: atom
path: atom.xml
limit: 20
```

将订阅添加到菜单栏中

* 找到 ``\next\_config.yml`` 下的 ``menu`` ， 把 ``rss`` 加进去。

```
menu:
  home: /
  rss: 

```

* 然后在下面 ``menu_icons`` 中加入你想让其显示的图标[图标传送](http://fontawesome.io/icons/)

```
menu_icons:
  logs: th-list
  projects: ra
  rss: rss
```

* 在 `/themes/hexo-theme-next/languages/zh-Hans.yml` 文件中（这里默认你使用的是简体中文，若是其他语言更改相应的yml就行），在 ``memu`` 下加一句即可：

```
menu:
  home: 首页
  archives: 归档
  categories: 分类
  tags: 标签
  about: 关于
  search: 搜索
  schedule: 日程表
  sitemap: 站点地图
  commonweal: 公益404
  logs: 日志
  projects: 项目
  rss: 订阅
```

###### MathJax支持

https://github.com/hexojs/hexo-math

#### 错误解答

##### 关于网站图标不更新问题

可以查看下GitHub网站上图标是否更新，因为git提交时忽略大小写的，可能文件没有更新，先将图标文件删除，在重新上传就可以了。




发表地址

* https://www.ttxxly.top/2018/08/02/hexo%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE/
* https://www.jianshu.com/p/6561f1b15c59
* 微信公众号-darklovy
* https://blog.csdn.net/jdliyao/article/details/81411951

发表时间

```
2018年8月4日16:00:28
```

