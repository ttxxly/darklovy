Application 和 Activity、service一样是 Android 框架的一个系统组件，当 Android 程序启动时系统会创建一个对象，用于存储系统的一些信息。

Android 系统会自动为每个程序运行时创建一个 Application 类并且只创建一个，所以 Application 可以说是单例模式（Singleton）的一个类。

在一般情况下我们是不需要指定一个 Application 的， 系统会自动为我们创建一个，如果我们需要自己创建一个Application，大致需要以下几个步骤：

* 创建一个类继承 Application
* 在 AndroidManifest.xml 中的 Application 标签中进行注册（只需给 Application 标签增加 name 属性，并且添加自己的 Application 名字）

在启动 Application 时，系统会创建一个 PID即进程ID， 所有的 Activity都会在此进程上运行。那么我们在 Application 创建的时候初始化全局变量，同一个应用的所有 Activity 都可以取到这些全局变量的值，换句话说，我们在 某一个 Activity 中改变了这些全局变量的值，那么在同一个应用的其其他 Activity 中值就会改变。

Application 对象的生命周期是整个程序中最长的，它的生命周期就等于这个程序的生命周期。因为它是全局单例的。

在不同的 Activity、Service 中获得的对象都是同一个对象。

#### 应用场景

* 实现应用程序级的全局变量，这种全局变量方法相对于静态类更有保障，知道应用的所有 Activity 全部被 Destory 才会被释放掉。
* 主题设置

##### 参考

* http://www.cnblogs.com/renqingping/archive/2012/10/24/Application.html