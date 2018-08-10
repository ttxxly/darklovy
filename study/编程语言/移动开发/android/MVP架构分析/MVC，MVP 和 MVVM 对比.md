### MVC 架构

![](http://image.beekka.com/blog/2015/bg2015020105.png)

```
* 视图（View）：用户界面
* 控制器（controller）：业务逻辑
* 模型（Model）：数据保存

各部分之间通信方式：
	* View 传送指令到 controller
	* controller 完成业务逻辑后，要求 Model 改变状态
	* Model 将新的数据发送到 View， 用户得到反馈
	
我们可以看到的是所有的通信是单向的。
```

### MVP 架构

![](http://image.beekka.com/blog/2015/bg2015020109.png)

```
* 各部分之间的通信是双向的。
* View 和 Model 不直接发生联系， 都通过 Presenter 传递
* 所有的逻辑都部署在 Presenter
```

### MVVM 架构

![](http://image.beekka.com/blog/2015/bg2015020110.png)

```
它采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel，反之亦然。Angular 和 Ember 都采用这种模式。
```



### 参考

* http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html