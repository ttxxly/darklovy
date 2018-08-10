Android 四大组件分别为 Activity、service、content provider、broadcast receiver。

#### Android 四大组件简介

* Activity：一个Activity通常就是一个单独的窗口，Activity之间通过Intent进行通信。Android应用中每一个Activity都必须要在AndroidMainfest.xml 配置文件中声明，否则系统将不能识别也不执行该Activity。

* service：用于在后台完成用户指定的操作。

* content provider：内容提供者，实现多个应用之间共享数据。

* broadcast receiver：广播接受者，对外部事件进行过滤，只对感兴趣的外部事件（电话呼入时、数据网络可用时）进行接收并作出相应，

  ​