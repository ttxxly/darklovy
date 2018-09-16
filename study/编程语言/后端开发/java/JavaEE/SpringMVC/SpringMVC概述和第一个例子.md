Spring MVC是当前最优秀的MVC框架，自从Spring 2.5版本发布后，由于支持注解配置，易用性有了大幅度的提高。Spring 3.0更加完善，实现了对老牌的MVC框架Struts 2的超越。现在版本已经到了Spring5.x了，我们这门课程是基于Spring5.0.6的SpringMVC框架来写案例。现在越来越多的开发团队选择了Spring MVC。

先写一个例子感受一下SpringMVC：

步骤1、新建Maven的web工程，加入jar包

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/8920f952f22e4b3faeca6b9d5f2204a9/clipboard.png)

步骤2、在web.xml中配置DispatcherServlet

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/7a2492ef23f54d75ac64d437ec64a621/clipboard.png)

选择后修改：

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/3719de67e84d402aae6892c39280ecf6/clipboard.png)

步骤3、加入SpringMVC的配置文件

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/2a67c92d1dad4b509d93bbcbeac88708/clipboard.png)



![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/830dde5de530400d8605717ca1ff4e5f/clipboard.png)

步骤4、编写Controller类

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/ec7d4ad3ad554bf5bbbbd20c43a39fa1/clipboard.png)

注意：这里RequestMapping的参数value处理可以是字符串数组，可以是字符串，前面讲过，当注解的value参数只有一个值的时候，还差将value=省略！ 这个不要忘记了！

步骤5、编写Jsp文件

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/2c58f0810ace4a2ca73a315d51eab00c/clipboard.png)



这个例子的大致流程分析：

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/0075501fb8a9460d90bd193b1059203f/clipboard.png)

![img](D:/Program%20Files%20%28x86%29/Youdao/YoudaoNote/data/qq4E1DE00B6AF3A13FEF9FAA509BA5B08E/31c94f89c7ba42b8895464bb2c6edb7b/clipboard.png)

