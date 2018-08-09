线程我不是很熟悉，努力学习中。

#### 相关面试题

##### 1. 下列有关Thread的描述，哪个是正确的？

```
A. 启动一个线程的方法是：thread. run()
B. 结束一个线程的通常做法是：thread. stop()
C. 将一个线程标记成daemon线程，意味着当主线程结束，
	并且没有其它正在运行的非daemon线程时，该daemon线程也会自动结束。
D. 让一个线程等待另一个线程的通知的方法是：thread. sleep()
```

```
解析：正确答案: C 
    A. 启动线程方法start();
    B. 线程stop方法已经被弃用；
    C. 守护线程在非守护线程结束后，会自动结束；
    D. 等待其他线程通知方法是wait()
```

##### 2. 有以下程序段， 则下面正确的选项是（）

```
public class MyThead extends Thread{
	public static void main(String[] args) {
		MyThead t=new MyThead();
		MyThead s=new MyThead();
		t.start();
		System.out.println("one.");
		s.start();
		System.out.println("two.");
	}
	public void run() {
		System.out.println("Thread");
	}
}
A. 编译失败
B. 程序运行可能结果为：
    one.
    Thread
    two.
    Thread
C. 程序运行可能结果是：
    one.
    two.
    Thread
    Thread
D. 程序运行结果不稳定
```

```
解析：
    start()是开启线程，等待获得时间片，一到获得时间片就执行。
        1. 可能一开启就获得了时间片执行。
        2. 可能等到two输出后才获得了时间片。
    所以 B C D 都有可能
```

##### 3. 下列代码执行结果为（ ）

```
public static void main(String argv[])throws InterruptedException{
	Thread t=new Thread(new Runnable() {
		public void run() {
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
            System.out.print("2");
		}
	});
	t.start();

	t.join();
	System.out.print("1");
}

A. 21
B. 12
C. 可能为12，也可能为21
D. 以上答案都不对
```

```
解析：答案：A
	thread.Join把指定的线程加入到当前线程，可以将两个交替执行的线程合并为顺序执行的线程。
	比如在线程B中调用了线程A的Join()方法，直到线程A执行完毕后，才会继续执行线程B。
    t.join();      //线程 t 执行完后才接着顺序执行
    t.join(1000);  //等待 t 线程，等待时间是1000毫秒
```

##### 4. 下面程序的运行结果：（ ）

```
public static void main(String args[]) {
	Thread t=new Thread(){
		public void  run(){
			dianping();
		}
    };
    t.run();
    System.out.print("dazhong");
}
static void dianping(){
	System.out.print("dianping");
}
A. dazhongdianping
B. dianpingdazhong
C. a和b都有可能
D. dianping循环输出，dazhong夹杂在中间
```

```
解析：答案：B
    在上面main()方法中，并没有创建一个新的线程，只是简单地方法调用而已。
    如果想要创建线程，需要t.start();创建线程，等待cpu时间片。
    run()方法只是简单地方法调用，所以先执行run()，在输出dazhong
```

##### 5. 以下程序运行的结果为 ( )

```
public class Example extends Thread{
    @Override
    public void run(){
		try{
			Thread.sleep(1000);
		}catch (InterruptedException e){
			e.printStackTrace();
		}
	System.out.print("run");
	}
    public static void main(String[] args){
		Example example=new Example();
		example.run();
		System.out.print("main");
	}
}
A. run main
B. main run
C. main
D. run
E. 不能确定
```

```
解析：答案：A
    创建一个线程需要覆盖Thread类的run方法，然后调用Thread类的start()方法启动
    这里直接调用run()方法并没有创建线程，跟普通方法调用一样，是顺序执行的
```

##### 6. 下列程序的运行结果正确的是（ ）

```
public static void main(String args[]) {
	Thread t = new Thread() {
        public void run() {
            pong();
        }
    };
    t.run();
    System.out.print("ping");
}
static void pong() {
	System.out.print("pong");
}

A. pingpong
B. pongping
C. pingpong和pongping都有可能
D. 都不输出
```

```
解析：答案：B
	注意Thread中start和run方法的区别
	start：真正启动线程，线程处于就绪状态。
		一旦得到时间片，则会调用线程的run方法进入运行状态，
	run：只是普通方法。
		直接调用调用run方法，程序就智慧按照顺序执行主线程这一个线程的。
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79837324