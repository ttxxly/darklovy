#### 相关面试题

```
1. Android系统对下列哪些对象提供了资源池 (A C)
    A. Message
    B. Thread
    C. AsyncTask
    D. Looper
    解析：
    	A.Message提供了消息池，有静态方法Obtain从消息池中取对象；
    	B.Thread默认不提供资源池，除非使用线程池ThreadPool管理；
    	C.AsynTask是线程池改造的。
    		池里 默认提供（核数+1）个线程进行并发操作
    		最大支持（核数  * 2 + 1）个线程，超过后会丢弃其他任务
    	D.Looper，每个Looper创建时创建一个消息队列和线程对象，也不是资源池；
```

