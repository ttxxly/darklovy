官方地址：https://docs.oracle.com/javase/7/docs/api/java/nio/channels/Pipe.html

java 管道为运行在同一个JVM中的两个线程提供了通信的能力。

在java中通信的双方应该是运行在同一进程中的不同线程。

Java提供管道功能，实现管道通信的类有两组：PipedInputStream和PipedOutputStream或者是PipedReader和PipedWriter。管道通信主要用于不同线程间的通信。

一个PipedInputStream实例对象必须和一个PipedOutputStream实例对象进行连接而产生一个通信管道。PipedOutputStream向管道中写入数据，PipedIntputStream读取PipedOutputStream向管道中写入的数据。一个线程的PipedInputStream对象能够从另外一个线程的PipedOutputStream对象中读取数据。

Java NIO 管道是 2 个线程之间的单向数据连接。Pipe有一个 source 通道和一个 sink 通道。数据会被写到 sink 通道，从 source 通道读取。

这里是 Pipe 原理的图示：

![img](http://wiki.jikexueyuan.com/project/java-nio/images/8.png)

#### 创建管道

通过Pipe.open()方法打开管道。例如：

`Pipe pipe = Pipe.open();`

#### 向管道写数据

要向管道写数据，需要访问 sink 通道。像这样：

`Pipe.SinkChannel sinkChannel = pipe.sink();`

通过调用 SinkChannel 的write()方法，将数据写入SinkChannel, 像这样：

```
String newData = "New String to write to file..." + System.currentTimeMillis();
ByteBuffer buf = ByteBuffer.allocate(48);
buf.clear();
buf.put(newData.getBytes());
buf.flip();
while(buf.hasRemaining()) {
    sinkChannel.write(buf);
}
```

#### 从管道读取数据

从读取管道的数据，需要访问 source 通道，像这样：

`Pipe.SourceChannel sourceChannel = pipe.source();`

调用 source 通道的read()方法来读取数据，像这样：

```
ByteBuffer buf = ByteBuffer.allocate(48);
int bytesRead = sourceChannel.read(buf);
```

read()方法返回的 int 值会告诉我们多少字节被读进了缓冲区。

#### 相关面试题

##### 1. 下列关于管道（Pipe）通信的叙述中，正确的是（ ）？

```
A. 进程对管道进行读操作和写操作都可能被阻塞
B. 一个管道只能有一个进程或一个写进程对其操作
C. 一个管道可实现双向数据传输
D. 管道的容量仅受磁盘容量大小限制
```

```
解析：
    A. 管道为空时，读操作会被阻塞；管道满时，写操作会被阻塞
    B. 可以有多个进程读写，只是不能同时写。
    C. 匿名管道只能单向，命名管道可以双向。
    D. 管道是在内存中。
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79836882