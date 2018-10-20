---
title: Java 面试题系列篇-虚拟机
date: 2018-10-20 18:15:37
tags: Java
---

## 虚拟机 （JVM）

### 【JVM】**你知道哪些或者你们线上使⽤什么GC策略？它有什么优势，适⽤于什么场景？**

https://blog.csdn.net/chenleixing/article/details/46706039/

### 【JVM】**Java类加载器包括⼏种？它们之间的⽗⼦关系是怎么样的？双亲委派机制是什么意思？有什么好处？**

启动Bootstrap类加载、扩展Extension类加载、系统System类加载。

父子关系如下：

启动类加载器 ，由C++ 实现，没有父类；

 

扩展类加载器，由Java语言实现，父类加载器为null；

 

系统类加载器，由Java语言实现，父类加载器为扩展类加载器；

 

自定义类加载器，父类加载器肯定为AppClassLoader。

 

双亲委派机制：类加载器收到类加载请求，自己不加载，向上委托给父类加载，父类加载不了，再自己加载。

 

优势避免Java核心API篡改。

 

https://blog.csdn.net/javazejian/article/details/73413292/

### 【JVM】**如何⾃定义⼀个类加载器？你使⽤过哪些或者你在什么场景下需要⼀个⾃定义的类加载器吗？**

自定义类加载的意义：

 

加载特定路径的class文件

 

加载一个加密的网络class文件

 

热部署加载class文件

### 【JVM】**jstack 是⼲什么的? jstat 呢？如果线上程序周期性地出现卡顿，你怀疑可 能是 GC 导致的，你会怎么来排查这个问题？线程⽇志⼀般你会看其中的什么 部分？**

jstack 用来查询 Java 进程的堆栈信息。

 

jvisualvm 监控内存泄露，跟踪垃圾回收、执行时内存、cpu分析、线程分析。

 

详见Java jvisualvm简要说明，可参考 线上FullGC频繁的排查。

 

Java jvisualvm简要说明

 

https://blog.csdn.net/a19881029/article/details/8432368/

 

线上FullGC频繁的排查

 

https://blog.csdn.net/wilsonpeng3/article/details/70064336/

### 【JVM】**StackOverflow异常有没有遇到过？⼀般你猜测会在什么情况下被触发？如何指定⼀个线程的堆栈⼤⼩？⼀般你们写多少？**

 

栈内存溢出，一般由栈内存的局部变量过爆了，导致内存溢出。出现在递归方法，参数个数过多，递归过深，递归没有出口。

### 什么是垃圾回收？

 

垃圾回收是Java中自动内存管理的另一种叫法。垃圾回收的目的是为程序保持尽可能多的可用堆（heap）。 JVM会删除堆上不再需要从堆引用的对象。

 

### 用一个例子解释垃圾回收？

 

比方说，下面这个方法就会从函数调用。

 

void method(){

​    Calendar calendar = new GregorianCalendar(2000,10,30);

​    System.out.println(calendar);

}

通过函数第一行代码中参考变量calendar，在堆上创建了GregorianCalendar类的一个对象。

 

函数结束执行后，引用变量calendar不再有效。因此，在方法中没有创建引用到对象。

 

JVM认识到这一点，会从堆中删除对象。这就是所谓的垃圾回收。

 

### 什么时候运行垃圾回收？

 

垃圾回收在JVM突发奇想和心血来潮时运行（没有那么糟糕）。运行垃圾收集的可能情况是：

 

堆可用内存不足

CPU空闲

 

### 垃圾回收的最佳做法？

 

用编程的方式，我们可以要求（记住这只是一个请求——不是一个命令）JVM通过调用System.gc()方法来运行垃圾回收。

 

当内存已满，且堆上没有对象可用于垃圾回收时，JVM可能会抛出OutOfMemoryException。

 

对象在被垃圾回收从堆上删除之前，会运行finalize()方法。我们建议不要用finalize()方法写任何代码。

### Java 中会存在内存泄漏吗，请简单描述。 

答：理论上Java因为有垃圾回收机制（GC）不会存在内存泄露问题（这也是Java被广泛使用于服务器端编程的一个重要原因）；然而在实际开发中，可能会存在无用但可达的对象，这些对象不能被GC回收，因此也会导致内存泄露的发生。例如Hibernate的Session（一级缓存）中的对象属于持久态，垃圾回收器是不会回收这些对象的，然而这些对象中可能存在无用的垃圾对象，如果不及时关闭（close）或清空（flush）一级缓存就可能导致内存泄露。下面例子中的代码也会导致内存泄露。

import java.util.Arrays;

import java.util.EmptyStackException;

 

public class MyStack<T> {

​    private T[] elements;

​    private int size = 0;

 

​    private static final int INIT_CAPACITY = 16;

 

​    public MyStack() {

​        elements = (T[]) new Object[INIT_CAPACITY];

​    }

 

​    public void push(T elem) {

​        ensureCapacity();

​        elements[size++] = elem;

​    }

 

​    public T pop() {

​        if(size == 0) 

​            throw new EmptyStackException();

​        return elements[--size];

​    }

 

​    private void ensureCapacity() {

​        if(elements.length == size) {

​            elements = Arrays.copyOf(elements, 2 * size + 1);

​        }

​    }

}

上面的代码实现了一个栈（先进后出（FILO））结构，乍看之下似乎没有什么明显的问题，它甚至可以通过你编写的各种单元测试。然而其中的pop方法却存在内存泄露的问题，当我们用pop方法弹出栈中的对象时，该对象不会被当作垃圾回收，即使使用栈的程序不再引用这些对象，因为栈内部维护着对这些对象的过期引用（obsolete reference）。在支持垃圾回收的语言中，内存泄露是很隐蔽的，这种内存泄露其实就是无意识的对象保持。如果一个对象引用被无意识的保留起来了，那么垃圾回收器不会处理这个对象，也不会处理该对象引用的其他对象，即使这样的对象只有少数几个，也可能会导致很多的对象被排除在垃圾回收之外，从而对性能造成重大影响，极端情况下会引发Disk Paging（物理内存与硬盘的虚拟内存交换数据），甚至造成OutOfMemoryError。

### GC是什么？为什么要有GC？ 

答：GC是垃圾收集的意思，内存处理是编程人员容易出现问题的地方，忘记或者错误的内存回收会导致程序或系统的不稳定甚至崩溃，Java提供的GC功能可以自动监测对象是否超过作用域从而达到自动回收内存的目的，Java语言没有提供释放已分配内存的显示操作方法。Java程序员不用担心内存管理，因为垃圾收集器会自动进行管理。要请求垃圾收集，可以调用下面的方法之一：System.gc() 或Runtime.getRuntime().gc() ，但JVM可以屏蔽掉显示的垃圾回收调用。 
垃圾回收可以有效的防止内存泄露，有效的使用可以使用的内存。垃圾回收器通常是作为一个单独的低优先级的线程运行，不可预知的情况下对内存堆中已经死亡的或者长时间没有使用的对象进行清除和回收，程序员不能实时的调用垃圾回收器对某个对象或所有对象进行垃圾回收。在Java诞生初期，垃圾回收是Java最大的亮点之一，因为服务器端的编程需要有效的防止内存泄露问题，然而时过境迁，如今Java的垃圾回收机制已经成为被诟病的东西。移动智能终端用户通常觉得iOS的系统比Android系统有更好的用户体验，其中一个深层次的原因就在于Android系统中垃圾回收的不可预知性。

补充：垃圾回收机制有很多种，包括：分代复制垃圾回收、标记垃圾回收、增量垃圾回收等方式。标准的Java进程既有栈又有堆。栈保存了原始型局部变量，堆保存了要创建的对象。Java平台对堆内存回收和再利用的基本算法被称为标记和清除，但是Java对其进行了改进，采用“分代式垃圾收集”。这种方法会跟Java对象的生命周期将堆内存划分为不同的区域，在垃圾收集过程中，可能会将对象移动到不同区域： 

- 伊甸园（Eden）：这是对象最初诞生的区域，并且对大多数对象来说，这里是它们唯一存在过的区域。 
- 幸存者乐园（Survivor）：从伊甸园幸存下来的对象会被挪到这里。 
- 终身颐养园（Tenured）：这是足够老的幸存对象的归宿。年轻代收集（Minor-GC）过程是不会触及这个地方的。当年轻代收集不能把对象放进终身颐养园时，就会触发一次完全收集（Major-GC），这里可能还会牵扯到压缩，以便为大对象腾出足够的空间。

与垃圾回收相关的JVM参数：

-Xms / -Xmx — 堆的初始大小 / 堆的最大大小

-Xmn — 堆中年轻代的大小

-XX:-DisableExplicitGC — 让System.gc()不产生任何作用

-XX:+PrintGCDetails — 打印GC的细节

-XX:+PrintGCDateStamps — 打印GC操作的时间戳

-XX:NewSize / XX:MaxNewSize — 设置新生代大小/新生代最大大小

-XX:NewRatio — 可以设置老生代和新生代的比例

-XX:PrintTenuringDistribution — 设置每次新生代GC后输出幸存者乐园中对象年龄的分布

-XX:InitialTenuringThreshold / -XX:MaxTenuringThreshold：设置老年代阀值的初始值和最大值

-XX:TargetSurvivorRatio：设置幸存区的目标使用率