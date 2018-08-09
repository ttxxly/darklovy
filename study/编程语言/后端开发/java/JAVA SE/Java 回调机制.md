在一个应用系统中，无论使用何种语言开发，必然会存在模块间的调用，调用的方式分为几种：

（1）同步调用:阻塞，单向

![](http://images2015.cnblogs.com/blog/801753/201702/801753-20170221201001413-1766758208.png)

同步调用是最基本并且最简单的一种调用方式。

类 A 的方法 a() 调用类 B 的方法 b()，一直等待 b() 方法执行完毕， a() 方法才对继续执行。

**适用于方法 b() 执行时间不长的情况（b() 方法执行时间过长或者直接阻塞，a() 的余下代码将无法执行，造成整个流程的阻塞）**

（2）异步调用：通过异步消息进行通知

![](http://images2015.cnblogs.com/blog/801753/201702/801753-20170221201512429-1532730453.png)

异步调用是为了解决同步调用可能出现阻塞，导致整个流程卡住而产生的一种调用方式。

**类A的方法方法a()通过新起线程的方式调用类B的方法b()，代码接着直接往下执行**

这样无论方法b()执行时间多久，都不会阻塞住方法a()的执行。但是这种方式，由于方法a()不等待方法b()的执行完成，在方法a()需要方法b()执行结果的情况下（视具体业务而定，有些业务比如启异步线程发个微信通知、刷新一个缓存这种就没必要），必须通过一定的方式对方法b()的执行结果进行监听。

在Java中，可以使用Future+Callable的方式来监听 b() 方法的执行结果。

（3）回调：双向

![](http://images2015.cnblogs.com/blog/801753/201702/801753-20170221205712070-824897248.png)

回调的思想

* **类A的a()方法调用类B的b()方法** 
* **类B的b()方法执行完毕主动调用类A的callback()方法** 

### 异步回调

模拟场景：客户端发送 msg 给服务器，服务器处理后（5s），回调给客户端，告知处理成功。

回调接口类：

```
/**
 * @author Jeff Lee
 * @since 2015-10-21 21:34:21
 * 回调模式-回调接口类
 */
public interface CSCallBack {
    public void process(String status);
}
```

模拟客户端

```
/**
 * @author Jeff Lee
 * @since 2015-10-21 21:25:14
 * 回调模式-模拟客户端类
 */
public class Client implements CSCallBack {
 
    private Server server;
 
    public Client(Server server) {
        this.server = server;
    }
 
    public void sendMsg(final String msg){
        System.out.println("客户端：发送的消息为：" + msg);
        new Thread(new Runnable() {
            @Override
            public void run() {
                server.getClientMsg(Client.this,msg);
            }
        }).start();
        System.out.println("客户端：异步发送成功");
    }
 
    @Override
    public void process(String status) {
        System.out.println("客户端：服务端回调状态为：" + status);
    }
}
```

模拟服务器

```
/**
 * @author Jeff Lee
 * @since 2015-10-21 21:24:15
 * 回调模式-模拟服务端类
 */
public class Server {
 
    public void getClientMsg(CSCallBack csCallBack , String msg) {
        System.out.println("服务端：服务端接收到客户端发送的消息为:" + msg);
 
        // 模拟服务端需要对数据处理
        try {
            Thread.sleep(5 * 1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("服务端:数据处理成功，返回成功状态 200");
        String status = "200";
        csCallBack.process(status);
    }
}
```

测试类

```
/**
 * @author Jeff Lee
 * @since 2015-10-21 21:24:15
 * 回调模式-测试类
 */
public class CallBackTest {
    public static void main(String[] args) {
        Server server = new Server();
        Client client = new Client(server);
 
        client.sendMsg("Server,Hello~");
    }
}
```

输出结果

```
客户端：发送的消息为：Server,Hello~
客户端：异步发送成功
服务端：服务端接收到客户端发送的消息为:Server,Hello~ （这里模拟服务端对数据处理时间，等待5秒）
服务端：数据处理成功，返回成功状态 200
客户端：服务端回调状态为：200
```

小结：

​	1、接口作为方法参数，其实际传入引用指向的是实现类 

​	2、Client的sendMsg方法中，参数为final，因为要被内部类一个新的线程可以使用。这里就体现了异步。 

​	3、调用server的getClientMsg()，参数传入了Client本身（对应第一点）。





### 参考

* http://www.cnblogs.com/heshuchao/p/5376298.html