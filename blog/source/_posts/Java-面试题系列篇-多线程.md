---
title: Java 面试题系列篇-多线程
date: 2018-10-20 18:10:10
tags: Java
---

## 多线程

### 什么是线程？

线程是操作系统能够进行运算调度的最小单位，它被包含在进程之中，是进程中的实际运作单位，可以使用多线程对进行运算提速。

比如，如果一个线程完成一个任务要100毫秒，那么用十个线程完成改任务只需10毫秒

### 什么是线程安全和线程不安全？

通俗的说：加锁的就是是线程安全的，不加锁的就是是线程不安全的

线程安全

线程安全: 就是多线程访问时，采用了加锁机制，当一个线程访问该类的某个数据时，进行保护，其他线程不能进行访问，直到该线程读取完，其他线程才可使用。不会出现数据不一致或者数据污染。

一个线程安全的计数器类的同一个实例对象在被多个线程使用的情况下也不会出现计算失误。很显然你可以将集合类分成两组，线程安全和非线程安全的。 Vector 是用同步方法来实现线程安全的, 而和它相似的ArrayList不是线程安全的。

线程不安全

线程不安全：就是不提供数据访问保护，有可能出现多个线程先后更改数据造成所得到的数据是脏数据

如果你的代码所在的进程中有多个线程在同时运行，而这些线程可能会同时运行这段代码。如果每次运行结果和单线程运行的结果是一样的，而且其他的变量的值也和预期的是一样的，就是线程安全的。

线程安全问题都是由全局变量及静态变量引起的。 若每个线程中对全局变量、静态变量只有读操作，而无写操作，一般来说，这个全局变量是线程安全的；若有多个线程同时执行写操作，一般都需要考虑线程同步，否则的话就可能影响线程安全。

 

### 什么是自旋锁？

基本概念

自旋锁是SMP架构中的一种low-level的同步机制。

当线程A想要获取一把自选锁而该锁又被其它线程锁持有时，线程A会在一个循环中自选以检测锁是不是已经可用了。

自选锁需要注意：

由于自旋时不释放CPU，因而持有自旋锁的线程应该尽快释放自旋锁，否则等待该自旋锁的线程会一直在那里自旋，这就会浪费CPU时间。

持有自旋锁的线程在sleep之前应该释放自旋锁以便其它线程可以获得自旋锁。

实现自旋锁

参考

segmentfault.com/q/101000000…

一个简单的while就可以满足你的要求。

目前的JVM实现自旋会消耗CPU，如果长时间不调用doNotify方法，doWait方法会一直自旋，CPU会消耗太大。

public class MyWaitNotify3{

 

  MonitorObject myMonitorObject = new MonitorObject();

  boolean wasSignalled = false;

 

  public void doWait(){

​    synchronized(myMonitorObject){

​      while(!wasSignalled){

​        try{

​          myMonitorObject.wait();

​         } catch(InterruptedException e){...}

​      }

​      //clear signal and continue running.

​      wasSignalled = false;

​    }

  }

 

  public void doNotify(){

​    synchronized(myMonitorObject){

​      wasSignalled = true;

​      myMonitorObject.notify();

​    }

  }

}

### 什么是Java内存模型？

Java内存模型描述了在多线程代码中哪些行为是合法的，以及线程如何通过内存进行交互。它描述了“程序中的变量“ 和 ”从内存或者寄存器获取或存储它们的底层细节”之间的关系。Java内存模型通过使用各种各样的硬件和编译器的优化来正确实现以上事情。

Java包含了几个语言级别的关键字，包括：volatile, final以及synchronized，目的是为了帮助程序员向编译器描述一个程序的并发需求。Java内存模型定义了volatile和synchronized的行为，更重要的是保证了同步的java程序在所有的处理器架构下面都能正确的运行。

“一个线程的写操作对其他线程可见”这个问题是因为编译器对代码进行重排序导致的。例如，只要代码移动不会改变程序的语义，当编译器认为程序中移动一个写操作到后面会更有效的时候，编译器就会对代码进行移动。如果编译器推迟执行一个操作，其他线程可能在这个操作执行完之前都不会看到该操作的结果，这反映了缓存的影响。

此外，写入内存的操作能够被移动到程序里更前的时候。在这种情况下，其他的线程在程序中可能看到一个比它实际发生更早的写操作。所有的这些灵活性的设计是为了通过给编译器，运行时或硬件灵活性使其能在最佳顺序的情况下来执行操作。在内存模型的限定之内，我们能够获取到更高的性能。

看下面代码展示的一个简单例子：

ClassReordering {

​    

​    int x = 0, y = 0;

   

​    public void writer() {

​        x = 1;

​        y = 2;

​    }

 

​    public void reader() {

​        int r1 = y;

​        int r2 = x;

​    }

}复制代码

让我们看在两个并发线程中执行这段代码，读取Y变量将会得到2这个值。因为这个写入比写到X变量更晚一些，程序员可能认为读取X变量将肯定会得到1。但是，写入操作可能被重排序过。如果重排序发生了，那么，就能发生对Y变量的写入操作，读取两个变量的操作紧随其后，而且写入到X这个操作能发生。程序的结果可能是r1变量的值是2，但是r2变量的值为0。

但是面试官，有时候不这么认为，认为就是JVM内存结构

JVM内存结构主要有三大块：堆内存、方法区和栈。

堆内存是JVM中最大的一块由年轻代和老年代组成，而年轻代内存又被分成三部分，Eden空间、From Survivor空间、To Survivor空间,默认情况下年轻代按照8:1:1的比例来分配；方法区存储类信息、常量、静态变量等数据，是线程共享的区域，为与Java堆区分，方法区还有一个别名Non-Heap(非堆)；栈又分为java虚拟机栈和本地方法栈主要用于方法的执行。

JAVA的JVM的内存可分为3个区：堆(heap)、栈(stack)和方法区(method)

java堆（Java Heap）

可通过参数 -Xms 和-Xmx设置

Java堆是被所有线程共享,是Java虚拟机所管理的内存中最大的一块 Java堆在虚拟机启动时创建。

Java堆唯一的目的是存放对象实例，几乎所有的对象实例和数组都在这里。

Java堆为了便于更好的回收和分配内存，可以细分为：新生代和老年代；再细致一点的有Eden空间、From Survivor空间、To Survivor区。

新生代：包括Eden区、From Survivor区、To Survivor区，系统默认大小Eden:Survivor=8:1。

老年代：在年轻代中经历了N次垃圾回收后仍然存活的对象，就会被放到年老代中。因此，可以认为年老代中存放的都是一些生命周期较长的对象。

Survivor空间等Java堆可以处在物理上不连续的内存空间中，只要逻辑上是连续的即可（就像我们的磁盘空间一样。在实现时，既可以实现成固定大小的，也可以是可扩展的）。

据Java虚拟机规范的规定，当方法区无法满足内存分配需求时，将抛出OutOfMemoryError异常。

java虚拟机栈(stack)

可通过参数 栈帧是方法运行期的基础数据结构栈容量可由-Xss设置

1.Java虚拟机栈是线程私有的，它的生命周期与线程相同。

每一个方法被调用直至执行完成的过程，就对应着一个栈帧在虚拟机栈中从入栈到出栈的过程。

虚拟机栈是执行Java方法的内存模型(也就是字节码)服务：每个方法在执行的同时都会创建一个栈帧，用于存储 局部变量表、操作数栈、动态链接、方法出口等信息。

局部变量表：32位变量槽，存放了编译期可知的各种基本数据类型、对象引用、returnAddress类型。

操作数栈：基于栈的执行引擎，虚拟机把操作数栈作为它的工作区，大多数指令都要从这里弹出数据、执行运算，然后把结果压回操作数栈。

动态连接：每个栈帧都包含一个指向运行时常量池（方法区的一部分）中该栈帧所属方法的引用。持有这个引用是为了支持方法调用过程中的动态连接。Class文件的常量池中有大量的符号引用，字节码中的方法调用指令就以常量池中指向方法的符号引用为参数。这些符号引用一部分会在类加载阶段或第一次使用的时候转化为直接引用，这种转化称为静态解析。另一部分将在每一次的运行期间转化为直接应用，这部分称为动态连接

方法出口：返回方法被调用的位置，恢复上层方法的局部变量和操作数栈，如果无返回值，则把它压入调用者的操作数栈。

 

局部变量表所需的内存空间在编译期间完成分配，当进入一个方法时，这个方法需要在帧中分配多大的局部变量空间是完全确定的。

 

 

在方法运行期间不会改变局部变量表的大小。主要存放了编译期可知的各种基本数据类型、对象引用 （reference类型）、returnAddress类型）。

 

java虚拟机栈,规定了两种异常状况：

如果线程请求的深度大于虚拟机所允许的深度，将抛出StackOverflowError异常。

如果虚拟机栈动态扩展，而扩展时无法申请到足够的内存，就会抛出OutOfMemoryError异常。

本地方法栈

可通过参数 栈容量可由-Xss设置

虚拟机栈为虚拟机执行Java方法（也就是字节码）服务。

本地方法栈则是为虚拟机使用到的Native方法服务。有的虚拟机（譬如Sun HotSpot虚拟机）直接就把本地方法栈和虚拟机栈合二为一

方法区（Method Area）

可通过参数-XX:MaxPermSize设置

 

线程共享内存区域，用于储存已被虚拟机加载的类信息、常量、静态变量，即编译器编译后的代码，方法区也称持久代（Permanent Generation）。

 

 

虽然Java虚拟机规范把方法区描述为堆的一个逻辑部分，但是它却有一个别名叫做Non-Heap（非堆），目的应该是与Java堆区分开来。

 

 

如何实现方法区，属于虚拟机的实现细节，不受虚拟机规范约束。

 

 

方法区主要存放java类定义信息，与垃圾回收关系不大，方法区可以选择不实现垃圾回收,但不是没有垃圾回收。

 

 

方法区域的内存回收目标主要是针对常量池的回收和对类型的卸载。

 

 

运行时常量池，也是方法区的一部分，虚拟机加载Class后把常量池中的数据放入运行时常量池。

 

运行时常量池

JDK1.6之前字符串常量池位于方法区之中。 JDK1.7字符串常量池已经被挪到堆之中。

可通过参数-XX:PermSize和-XX:MaxPermSize设置

常量池（Constant Pool）：常量池数据编译期被确定，是Class文件中的一部分。存储了类、方法、接口等中的常量，当然也包括字符串常量。

字符串池/字符串常量池（String Pool/String Constant Pool）：是常量池中的一部分，存储编译期类中产生的字符串类型数据。

运行时常量池（Runtime Constant Pool）：方法区的一部分，所有线程共享。虚拟机加载Class后把常量池中的数据放入到运行时常量池。常量池：可以理解为Class文件之中的资源仓库，它是Class文件结构中与其他项目资源关联最多的数据类型。

 

常量池中主要存放两大类常量：字面量（Literal）和符号引用（Symbolic Reference）。

 

 

字面量：文本字符串、声明为final的常量值等。

 

 

符号引用：类和接口的完全限定名（Fully Qualified Name）、字段的名称和描述符（Descriptor）、方法的名称和描述符。

 

直接内存

可通过-XX:MaxDirectMemorySize指定，如果不指定，则默认与Java堆的最大值（-Xmx指定）一样。

直接内存（Direct Memory）并不是虚拟机运行时数据区的一部分，也不是Java虚拟机规范中定义的内存区域，但是这部分内存也被频繁地使用，而且也可能导致OutOfMemoryError异常出现。

总结的简单一点

java堆（Java Heap）

可通过参数 -Xms 和-Xmx设置

Java堆是被所有线程共享,是Java虚拟机所管理的内存中最大的一块 Java堆在虚拟机启动时创建

Java堆唯一的目的是存放对象实例，几乎所有的对象实例和数组都在这里

Java堆为了便于更好的回收和分配内存，可以细分为：新生代和老年代；再细致一点的有Eden空间、From Survivor空间、To Survivor区

新生代：包括Eden区、From Survivor区、To Survivor区，系统默认大小Eden:Survivor=8:1。

老年代：在年轻代中经历了N次垃圾回收后仍然存活的对象，就会被放到年老代中。因此，可以认为年老代中存放的都是一些生命周期较长的对象。

java虚拟机栈(stack)

可通过参数 栈帧是方法运行期的基础数据结构栈容量可由-Xss设置

Java虚拟机栈是线程私有的，它的生命周期与线程相同。

每一个方法被调用直至执行完成的过程，就对应着一个栈帧在虚拟机栈中从入栈到出栈的过程。

虚拟机栈是执行Java方法的内存模型(也就是字节码)服务：每个方法在执行的同时都会创建一个栈帧，用于存储 局部变量表、操作数栈、动态链接、方法出口等信息

方法区（Method Area）

可通过参数-XX:MaxPermSize设置

 

线程共享内存区域），用于储存已被虚拟机加载的类信息、常量、静态变量，即编译器编译后的代码，方法区也称持久代（Permanent Generation）。

 

 

方法区主要存放java类定义信息，与垃圾回收关系不大，方法区可以选择不实现垃圾回收,但不是没有垃圾回收。

 

 

方法区域的内存回收目标主要是针对常量池的回收和对类型的卸载。

 

 

运行时常量池，也是方法区的一部分，虚拟机加载Class后把常量池中的数据放入运行时常量池。

 

### 什么是CAS？

CAS（compare and swap）的缩写，中文翻译成比较并交换。

CAS 不通过JVM,直接利用java本地方 JNI（Java Native Interface为JAVA本地调用）,直接调用CPU 的cmpxchg（是汇编指令）指令。

利用CPU的CAS指令，同时借助JNI来完成Java的非阻塞算法,实现原子操作。其它原子操作都是利用类似的特性完成的。

整个java.util.concurrent都是建立在CAS之上的，因此对于synchronized阻塞算法，J.U.C在性能上有了很大的提升。

CAS是项乐观锁技术，当多个线程尝试使用CAS同时更新同一个变量时，只有其中一个线程能更新变量的值，而其它线程都失败，失败的线程并不会被挂起，而是被告知这次竞争中失败，并可以再次尝试。

CAS应用

CAS有3个操作数，内存值V，旧的预期值A，要修改的新值B。当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做。

CAS优点

确保对内存的读-改-写操作都是原子操作执行

CAS缺点

CAS虽然很高效的解决原子操作，但是CAS仍然存在三大问题。ABA问题，循环时间长开销大和只能保证一个共享变量的原子操作

总结

使用CAS在线程冲突严重时，会大幅降低程序性能；CAS只适合于线程冲突较少的情况使用。

synchronized在jdk1.6之后，已经改进优化。synchronized的底层实现主要依靠Lock-Free的队列，基本思路是自旋后阻塞，竞争切换后继续竞争锁，稍微牺牲了公平性，但获得了高吞吐量。在线程冲突较少的情况下，可以获得和CAS类似的性能；而线程冲突严重的情况下，性能远高于CAS。

参考 blog.52itstyle.com/archives/94…

### 什么是乐观锁和悲观锁？

悲观锁

Java在JDK1.5之前都是靠synchronized关键字保证同步的，这种通过使用一致的锁定协议来协调对共享状态的访问，可以确保无论哪个线程持有共享变量的锁，都采用独占的方式来访问这些变量。独占锁其实就是一种悲观锁，所以可以说synchronized是悲观锁。

乐观锁

乐观锁（ Optimistic Locking）其实是一种思想。相对悲观锁而言，乐观锁假设认为数据一般情况下不会造成冲突，所以在数据进行提交更新的时候，才会正式对数据的冲突与否进行检测，如果发现冲突了，则让返回用户错误的信息，让用户决定如何去做。

### 什么是AQS？

AbstractQueuedSynchronizer简称AQS，是一个用于构建锁和同步容器的框架。事实上concurrent包内许多类都是基于AQS构建，例如ReentrantLock，Semaphore，CountDownLatch，ReentrantReadWriteLock，FutureTask等。AQS解决了在实现同步容器时设计的大量细节问题。

AQS使用一个FIFO的队列表示排队等待锁的线程，队列头节点称作“哨兵节点”或者“哑节点”，它不与任何线程关联。其他的节点与等待线程关联，每个节点维护一个等待状态waitStatus。

CAS 原子操作在concurrent包的实现

参考 blog.52itstyle.com/archives/94…

由于java的CAS同时具有 volatile 读和volatile写的内存语义，因此Java线程之间的通信现在有了下面四种方式：

A线程写volatile变量，随后B线程读这个volatile变量。

A线程写volatile变量，随后B线程用CAS更新这个volatile变量。

A线程用CAS更新一个volatile变量，随后B线程用CAS更新这个volatile变量。

A线程用CAS更新一个volatile变量，随后B线程读这个volatile变量。

Java的CAS会使用现代处理器上提供的高效机器级别原子指令，这些原子指令以原子方式对内存执行读-改-写操作，这是在多处理器中实现同步的关键（从本质上来说，能够支持原子性读-改-写指令的计算机器，是顺序计算图灵机的异步等价机器，因此任何现代的多处理器都会去支持某种能对内存执行原子性读-改-写操作的原子指令）。同时，volatile变量的读/写和CAS可以实现线程之间的通信。把这些特性整合在一起，就形成了整个concurrent包得以实现的基石。如果我们仔细分析concurrent包的源代码实现，会发现一个通用化的实现模式：

首先，声明共享变量为volatile； 然后，使用CAS的原子条件更新来实现线程之间的同步；

同时，配合以volatile的读/写和CAS所具有的volatile读和写的内存语义来实现线程之间的通信。

AQS，非阻塞数据结构和原子变量类（Java.util.concurrent.atomic包中的类），这些concurrent包中的基础类都是使用这种模式来实现的，而concurrent包中的高层类又是依赖于这些基础类来实现的。从整体来看，concurrent包的实现示意图如下：

 

AQS没有锁之类的概念，它有个state变量，是个int类型，在不同场合有着不同含义。

AQS围绕state提供两种基本操作“获取”和“释放”，有条双向队列存放阻塞的等待线程，并提供一系列判断和处理方法，简单说几点：

state是独占的，还是共享的；

state被获取后，其他线程需要等待；

state被释放后，唤醒等待线程；

线程等不及时，如何退出等待。

至于线程是否可以获得state，如何释放state，就不是AQS关心的了，要由子类具体实现。

AQS中还有一个表示状态的字段state，例如ReentrantLocky用它表示线程重入锁的次数，Semaphore用它表示剩余的许可数量，FutureTask用它表示任务的状态。对state变量值的更新都采用CAS操作保证更新操作的原子性。

AbstractQueuedSynchronizer继承了AbstractOwnableSynchronizer，这个类只有一个变量：exclusiveOwnerThread，表示当前占用该锁的线程，并且提供了相应的get，set方法。

ReentrantLock实现原理

www.cnblogs.com/maypattis/p…

### 什么是原子操作？在Java Concurrency API中有哪些原子类(atomic classes)？

原子操作是指一个不受其他操作影响的操作任务单元。原子操作是在多线程环境下避免数据不一致必须的手段。

int++并不是一个原子操作，所以当一个线程读取它的值并加1时，另外一个线程有可能会读到之前的值，这就会引发错误。

为了解决这个问题，必须保证增加操作是原子的，在JDK1.5之前我们可以使用同步技术来做到这一点。

到JDK1.5，java.util.concurrent.atomic包提供了int和long类型的装类，它们可以自动的保证对于他们的操作是原子的并且不需要使用同步。   

### 什么是Executors框架？

Executor框架同java.util.concurrent.Executor 接口在Java 5中被引入。

Executor框架是一个根据一组执行策略调用，调度，执行和控制的异步任务的框架。

无限制的创建线程会引起应用程序内存溢出。所以创建一个线程池是个更好的的解决方案，因为可以限制线程的数量并且可以回收再利用这些线程。

利用Executors框架可以非常方便的创建一个线程池，

Java通过Executors提供四种线程池，分别为：

newCachedThreadPool创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。

newFixedThreadPool 创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。

newScheduledThreadPool 创建一个定长线程池，支持定时及周期性任务执行。

newSingleThreadExecutor 创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。   

### 什么是阻塞队列？如何使用阻塞队列来实现生产者-消费者模型？

JDK7提供了7个阻塞队列。（也属于并发容器）

ArrayBlockingQueue ：一个由数组结构组成的有界阻塞队列。

LinkedBlockingQueue ：一个由链表结构组成的有界阻塞队列。

PriorityBlockingQueue ：一个支持优先级排序的无界阻塞队列。

DelayQueue：一个使用优先级队列实现的无界阻塞队列。

SynchronousQueue：一个不存储元素的阻塞队列。

LinkedTransferQueue：一个由链表结构组成的无界阻塞队列。

LinkedBlockingDeque：一个由链表结构组成的双向阻塞队列。

什么是阻塞队列？

阻塞队列是一个在队列基础上又支持了两个附加操作的队列。

2个附加操作：

支持阻塞的插入方法：队列满时，队列会阻塞插入元素的线程，直到队列不满。 支持阻塞的移除方法：队列空时，获取元素的线程会等待队列变为非空。

阻塞队列的应用场景

阻塞队列常用于生产者和消费者的场景，生产者是向队列里添加元素的线程，消费者是从队列里取元素的线程。简而言之，阻塞队列是生产者用来存放元素、消费者获取元素的容器。

几个方法

在阻塞队列不可用的时候，上述2个附加操作提供了四种处理方法

| 方法\处理方式 | 抛出异常  | 返回特殊值 | 一直阻塞 | 超时退出           |
| ------------- | --------- | ---------- | -------- | ------------------ |
| 插入方法      | add(e)    | offer(e)   | put(e)   | offer(e,time,unit) |
| 移除方法      | remove()  | poll()     | take()   | poll(time,unit)    |
| 检查方法      | element() | peek()     | 不可用   | 不可用             |

JAVA里的阻塞队列

JDK 7 提供了7个阻塞队列，如下

1、ArrayBlockingQueue 数组结构组成的有界阻塞队列。

此队列按照先进先出（FIFO）的原则对元素进行排序，但是默认情况下不保证线程公平的访问队列，即如果队列满了，那么被阻塞在外面的线程对队列访问的顺序是不能保证线程公平（即先阻塞，先插入）的。

2、LinkedBlockingQueue一个由链表结构组成的有界阻塞队列

此队列按照先出先进的原则对元素进行排序

3、PriorityBlockingQueue支持优先级的无界阻塞队列

4、DelayQueue支持延时获取元素的无界阻塞队列，即可以指定多久才能从队列中获取当前元素

5、SynchronousQueue不存储元素的阻塞队列，每一个put必须等待一个take操作，否则不能继续添加元素。并且他支持公平访问队列。

6、LinkedTransferQueue由链表结构组成的无界阻塞TransferQueue队列。相对于其他阻塞队列，多了tryTransfer和transfer方法

transfer方法

如果当前有消费者正在等待接收元素（take或者待时间限制的poll方法），transfer可以把生产者传入的元素立刻传给消费者。如果没有消费者等待接收元素，则将元素放在队列的tail节点，并等到该元素被消费者消费了才返回。

tryTransfer方法

用来试探生产者传入的元素能否直接传给消费者。，如果没有消费者在等待，则返回false。和上述方法的区别是该方法无论消费者是否接收，方法立即返回。而transfer方法是必须等到消费者消费了才返回。

7、LinkedBlockingDeque链表结构的双向阻塞队列，优势在于多线程入队时，减少一半的竞争。

如何使用阻塞队列来实现生产者-消费者模型？

通知模式实现：所谓通知模式，就是当生产者往满的队列里添加元素时会阻塞住生产者，当消费者消费了一个队列中的元素后，会通知生产者当前队列可用。

使用BlockingQueue解决生产者消费者问题

为什么BlockingQueue适合解决生产者消费者问题

任何有效的生产者-消费者问题解决方案都是通过控制生产者put()方法（生产资源）和消费者take()方法（消费资源）的调用来实现的，一旦你实现了对方法的阻塞控制，那么你将解决该问题。

Java通过BlockingQueue提供了开箱即用的支持来控制这些方法的调用（一个线程创建资源，另一个消费资源）。java.util.concurrent包下的BlockingQueue接口是一个线程安全的可用于存取对象的队列。

BlockingQueue是一种数据结构，支持一个线程往里存资源，另一个线程从里取资源。这正是解决生产者消费者问题所需要的，那么让我们开始解决该问题吧。

生产者

以下代码用于生产者线程

package io.ymq.example.thread;

import java.util.concurrent.BlockingQueue;

/**

- 描述:生产者

 *

- @author yanpenglei
- @create 2018-03-14 15:52

 **/class Producer implements Runnable {

 

​    protected BlockingQueue<Object> queue;

 

​    Producer(BlockingQueue<Object> theQueue) {

​        this.queue = theQueue;

​    }

 

​    public void run() {

​        try {

​            while (true) {

​                Object justProduced = getResource();

​                queue.put(justProduced);

​                System.out.println("生产者资源队列大小= " + queue.size());

​            }

​        } catch (InterruptedException ex) {

​            System.out.println("生产者 中断");

​        }

​    }

 

​    Object getResource() {

​        try {

​            Thread.sleep(100);

​        } catch (InterruptedException ex) {

​            System.out.println("生产者 读 中断");

​        }

​        return new Object();

​    }

}复制代码

消费者

以下代码用于消费者线程

package io.ymq.example.thread;

import java.util.concurrent.BlockingQueue;

/**

- 描述: 消费者

 *

- @author yanpenglei
- @create 2018-03-14 15:54

 **/class Consumer implements Runnable {

​    protected BlockingQueue<Object> queue;

 

​    Consumer(BlockingQueue<Object> theQueue) {

​        this.queue = theQueue;

​    }

 

​    public void run() {

​        try {

​            while (true) {

​                Object obj = queue.take();

​                System.out.println("消费者 资源 队列大小 " + queue.size());

​                take(obj);

​            }

​        } catch (InterruptedException ex) {

​            System.out.println("消费者 中断");

​        }

​    }

 

​    void take(Object obj) {

​        try {

​            Thread.sleep(100); // simulate time passing

​        } catch (InterruptedException ex) {

​            System.out.println("消费者 读 中断");

​        }

​        System.out.println("消费对象 " + obj);

​    }

}复制代码

测试该解决方案是否运行正常

package io.ymq.example.thread;import java.util.concurrent.BlockingQueue;import java.util.concurrent.LinkedBlockingQueue;

/**

- 描述: 测试

 *

- @author yanpenglei
- @create 2018-03-14 15:58

 **/public class ProducerConsumerExample {

 

​    public static void main(String[] args) throws InterruptedException {

 

​        int numProducers = 4;

​        int numConsumers = 3;

 

​        BlockingQueue<Object> myQueue = new LinkedBlockingQueue<Object>(5);

 

​        for (int i = 0; i < numProducers; i++) {

​            new Thread(new Producer(myQueue)).start();

​        }

 

​        for (int i = 0; i < numConsumers; i++) {

​            new Thread(new Consumer(myQueue)).start();

​        }

 

​        Thread.sleep(1000);

 

​        System.exit(0);

​    }

}复制代码

运行结果

生产者资源队列大小= 1

生产者资源队列大小= 1

消费者 资源 队列大小 1

生产者资源队列大小= 1

消费者 资源 队列大小 1

消费者 资源 队列大小 1

生产者资源队列大小= 1

生产者资源队列大小= 3

消费对象 java.lang.Object@1e1aa52b

生产者资源队列大小= 2

生产者资源队列大小= 5

消费对象 java.lang.Object@6e740a76

消费对象 java.lang.Object@697853f6

 

......

 

消费对象 java.lang.Object@41a10cbc

消费对象 java.lang.Object@4963c8d1

消费者 资源 队列大小 5

生产者资源队列大小= 5

生产者资源队列大小= 5

消费者 资源 队列大小 4

消费对象 java.lang.Object@3e49c35d

消费者 资源 队列大小 4

生产者资源队列大小= 5复制代码

从输出结果中,我们可以发现队列大小永远不会超过5，消费者线程消费了生产者生产的资源。

### 什么是Callable和Future?

Callable 和 Future 是比较有趣的一对组合。当我们需要获取线程的执行结果时，就需要用到它们。Callable用于产生结果，Future用于获取结果。

Callable接口使用泛型去定义它的返回类型。Executors类提供了一些有用的方法去在线程池中执行Callable内的任务。由于Callable任务是并行的，必须等待它返回的结果。java.util.concurrent.Future对象解决了这个问题。

在线程池提交Callable任务后返回了一个Future对象，使用它可以知道Callable任务的状态和得到Callable返回的执行结果。Future提供了get()方法，等待Callable结束并获取它的执行结果。

代码示例

Callable 是一个接口，它只包含一个call()方法。Callable是一个返回结果并且可能抛出异常的任务。

为了便于理解，我们可以将Callable比作一个Runnable接口，而Callable的call()方法则类似于Runnable的run()方法。

public class CallableFutureTest {

 

​    public static void main(String[] args) throws InterruptedException, ExecutionException {

 

​        System.out.println("start main thread ");

 

​        ExecutorService exec = Executors.newFixedThreadPool(2);

 

​        //新建一个Callable 任务，并将其提交到一个ExecutorService. 将返回一个描述任务情况的Future.

​        Callable<String> call = new Callable<String>() {

 

​            @Override

​            public String call() throws Exception {

​                System.out.println("start new thread ");

​                Thread.sleep(5000);

​                System.out.println("end new thread ");

​                return "我是返回的内容";

​            }

​        };

 

​        Future<String> task = exec.submit(call);

​        Thread.sleep(1000);

​        String retn = task.get();

​        //关闭线程池

​        exec.shutdown();

​        System.out.println(retn + "--end main thread");

​    }

}复制代码

控制台打印

start main thread 

start new thread 

end new thread 

我是返回的内容--end main thread复制代码

### 什么是FutureTask?

FutureTask可用于异步获取执行结果或取消执行任务的场景。通过传入Runnable或者Callable的任务给FutureTask，直接调用其run方法或者放入线程池执行，之后可以在外部通过FutureTask的get方法异步获取执行结果，因此，FutureTask非常适合用于耗时的计算，主线程可以在完成自己的任务后，再去获取结果。另外，FutureTask还可以确保即使调用了多次run方法，它都只会执行一次Runnable或者Callable任务，或者通过cancel取消FutureTask的执行等。

1.执行多任务计算

FutureTask执行多任务计算的使用场景

利用FutureTask和ExecutorService，可以用多线程的方式提交计算任务，主线程继续执行其他任务，当主线程需要子线程的计算结果时，在异步获取子线程的执行结果。

import java.util.ArrayList;import java.util.List;import java.util.concurrent.*;

public class FutureTaskForMultiCompute {

 

​    public static void main(String[] args) {

 

​        FutureTaskForMultiCompute inst = new FutureTaskForMultiCompute();

​        // 创建任务集合

​        List<FutureTask<Integer>> taskList = new ArrayList<FutureTask<Integer>>();

​        // 创建线程池

​        ExecutorService exec = Executors.newFixedThreadPool(5);

​        for (int i = 0; i < 10; i++) {

​            // 传入Callable对象创建FutureTask对象

​            FutureTask<Integer> ft = new FutureTask<Integer>(inst.new ComputeTask(i, "" + i));

​            taskList.add(ft);

​            // 提交给线程池执行任务，也可以通过exec.invokeAll(taskList)一次性提交所有任务;

​            exec.submit(ft);

​        }

 

​        System.out.println("所有计算任务提交完毕, 主线程接着干其他事情！");

 

​        // 开始统计各计算线程计算结果

​        Integer totalResult = 0;

​        for (FutureTask<Integer> ft : taskList) {

​            try {

​                //FutureTask的get方法会自动阻塞,直到获取计算结果为止

​                totalResult = totalResult + ft.get();

​            } catch (InterruptedException e) {

​                e.printStackTrace();

​            } catch (ExecutionException e) {

​                e.printStackTrace();

​            }

​        }

 

​        // 关闭线程池

​        exec.shutdown();

​        System.out.println("多任务计算后的总结果是:" + totalResult);

 

​    }

 

​    private class ComputeTask implements Callable<Integer> {

 

​        private Integer result = 0;

​        private String taskName = "";

 

​        public ComputeTask(Integer iniResult, String taskName) {

​            result = iniResult;

​            this.taskName = taskName;

​            System.out.println("生成子线程计算任务: " + taskName);

​        }

 

​        public String getTaskName() {

​            return this.taskName;

​        }

 

​        @Override

​        public Integer call() throws Exception {

​            // TODO Auto-generated method stub

 

​            for (int i = 0; i < 100; i++) {

​                result = +i;

​            }

​            // 休眠5秒钟，观察主线程行为，预期的结果是主线程会继续执行，到要取得FutureTask的结果是等待直至完成。

​            Thread.sleep(5000);

​            System.out.println("子线程计算任务: " + taskName + " 执行完成!");

​            return result;

​        }

​    }

}复制代码

生成子线程计算任务: 0

生成子线程计算任务: 1

生成子线程计算任务: 2

生成子线程计算任务: 3

生成子线程计算任务: 4

生成子线程计算任务: 5

生成子线程计算任务: 6

生成子线程计算任务: 7

生成子线程计算任务: 8

生成子线程计算任务: 9

所有计算任务提交完毕, 主线程接着干其他事情！

子线程计算任务: 0 执行完成!

子线程计算任务: 2 执行完成!

子线程计算任务: 3 执行完成!

子线程计算任务: 4 执行完成!

子线程计算任务: 1 执行完成!

子线程计算任务: 8 执行完成!

子线程计算任务: 7 执行完成!

子线程计算任务: 6 执行完成!

子线程计算任务: 9 执行完成!

子线程计算任务: 5 执行完成!

多任务计算后的总结果是:990复制代码

2.高并发环境下

FutureTask在高并发环境下确保任务只执行一次

在很多高并发的环境下，往往我们只需要某些任务只执行一次。这种使用情景FutureTask的特性恰能胜任。举一个例子，假设有一个带key的连接池，当key存在时，即直接返回key对应的对象；当key不存在时，则创建连接。对于这样的应用场景，通常采用的方法为使用一个Map对象来存储key和连接池对应的对应关系，典型的代码如下面所示：

  private Map<String, Connection> connectionPool = new HashMap<String, Connection>();

​    private ReentrantLock lock = new ReentrantLock();

 

​    public Connection getConnection(String key) {

​        try {

​            lock.lock();

​            if (connectionPool.containsKey(key)) {

​                return connectionPool.get(key);

​            } else {

​                //创建 Connection  

​                Connection conn = createConnection();

​                connectionPool.put(key, conn);

​                return conn;

​            }

​        } finally {

​            lock.unlock();

​        }

​    }

 

​    //创建Connection  

​    private Connection createConnection() {

​        return null;

​    }

复制代码

在上面的例子中，我们通过加锁确保高并发环境下的线程安全，也确保了connection只创建一次，然而确牺牲了性能。改用ConcurrentHash的情况下，几乎可以避免加锁的操作，性能大大提高，但是在高并发的情况下有可能出现Connection被创建多次的现象。这时最需要解决的问题就是当key不存在时，创建Connection的动作能放在connectionPool之后执行，这正是FutureTask发挥作用的时机，基于ConcurrentHashMap和FutureTask的改造代码如下：

  private ConcurrentHashMap<String, FutureTask<Connection>> connectionPool = new ConcurrentHashMap<String, FutureTask<Connection>>();

 

​    public Connection getConnection(String key) throws Exception {

​        FutureTask<Connection> connectionTask = connectionPool.get(key);

​        if (connectionTask != null) {

​            return connectionTask.get();

​        } else {

​            Callable<Connection> callable = new Callable<Connection>() {

​                @Override

​                public Connection call() throws Exception {

​                    // TODO Auto-generated method stub  

​                    return createConnection();

​                }

​            };

​            FutureTask<Connection> newTask = new FutureTask<Connection>(callable);

​            connectionTask = connectionPool.putIfAbsent(key, newTask);

​            if (connectionTask == null) {

​                connectionTask = newTask;

​                connectionTask.run();

​            }

​            return connectionTask.get();

​        }

​    }

 

​    //创建Connection  

​    private Connection createConnection() {

​        return null;

​    }复制代码

经过这样的改造，可以避免由于并发带来的多次创建连接及锁的出现。

### 什么是同步容器和并发容器的实现？

一、同步容器

主要代表有Vector和Hashtable，以及Collections.synchronizedXxx等。 锁的粒度为当前对象整体。 迭代器是及时失败的，即在迭代的过程中发现被修改，就会抛出ConcurrentModificationException。

二、并发容器

主要代表有ConcurrentHashMap、CopyOnWriteArrayList、ConcurrentSkipListMap、ConcurrentSkipListSet。 锁的粒度是分散的、细粒度的，即读和写是使用不同的锁。 迭代器具有弱一致性，即可以容忍并发修改，不会抛出ConcurrentModificationException。

JDK 7 ConcurrentHashMap

采用分离锁技术，同步容器中，是一个容器一个锁，但在ConcurrentHashMap中，会将hash表的数组部分分成若干段，每段维护一个锁，以达到高效的并发访问；

JDK 8 ConcurrentHashMap

采用分离锁技术，同步容器中，是一个容器一个锁，但在ConcurrentHashMap中，会将hash表的数组部分分成若干段，每段维护一个锁，以达到高效的并发访问；

三、阻塞队列

主要代表有LinkedBlockingQueue、ArrayBlockingQueue、PriorityBlockingQueue(Comparable,Comparator)、SynchronousQueue。 提供了可阻塞的put和take方法，以及支持定时的offer和poll方法。 适用于生产者、消费者模式（线程池和工作队列-Executor），同时也是同步容器

四、双端队列

主要代表有ArrayDeque和LinkedBlockingDeque。 意义：正如阻塞队列适用于生产者消费者模式，双端队列同样适用与另一种模式，即工作密取。在生产者-消费者设计中，所有消费者共享一个工作队列，而在工作密取中，每个消费者都有各自的双端队列。 如果一个消费者完成了自己双端队列中的全部工作，那么他就可以从其他消费者的双端队列末尾秘密的获取工作。具有更好的可伸缩性，这是因为工作者线程不会在单个共享的任务队列上发生竞争。 在大多数时候，他们都只是访问自己的双端队列，从而极大的减少了竞争。当工作者线程需要访问另一个队列时，它会从队列的尾部而不是头部获取工作，因此进一步降低了队列上的竞争。 适用于：网页爬虫等任务中

五、比较及适用场景

如果不需要阻塞队列，优先选择ConcurrentLinkedQueue； 如果需要阻塞队列，队列大小固定优先选择ArrayBlockingQueue，队列大小不固定优先选择LinkedBlockingQueue； 如果需要对队列进行排序，选择PriorityBlockingQueue； 如果需要一个快速交换的队列，选择SynchronousQueue； 如果需要对队列中的元素进行延时操作，则选择DelayQueue。

### 什么是多线程？优缺点？

什么是多线程？

多线程：是指从软件或者硬件上实现多个线程的并发技术。

多线程的好处：

使用多线程可以把程序中占据时间长的任务放到后台去处理，如图片、视屏的下载

发挥多核处理器的优势，并发执行让系统运行的更快、更流畅，用户体验更好

多线程的缺点：

大量的线程降低代码的可读性；

更多的线程需要更多的内存空间

当多个线程对同一个资源出现争夺时候要注意线程安全的问题。

### 什么是多线程的上下文切换？

即使是单核CPU也支持多线程执行代码，CPU通过给每个线程分配CPU时间片来实现这个机制。时间片是CPU分配给各个线程的时间，因为时间片非常短，所以CPU通过不停地切换线程执行，让我们感觉多个线程时同时执行的，时间片一般是几十毫秒（ms）

上下文切换过程中，CPU会停止处理当前运行的程序，并保存当前程序运行的具体位置以便之后继续运行

CPU通过时间片分配算法来循环执行任务，当前任务执行一个时间片后会切换到下一个任务。但是，在切换前会保存上一个任务的状态，以便下次切换回这个任务时，可以再次加载这个任务的状态

从任务保存到再加载的过程就是一次上下文切换

### ThreadLocal的设计理念与作用？

Java中的ThreadLocal类允许我们创建只能被同一个线程读写的变量。因此，如果一段代码含有一个ThreadLocal变量的引用，即使两个线程同时执行这段代码，它们也无法访问到对方的ThreadLocal变量

ThreadLocal

如何创建ThreadLocal变量

以下代码展示了如何创建一个ThreadLocal变量：

private ThreadLocal myThreadLocal = new ThreadLocal();复制代码

通过这段代码实例化了一个ThreadLocal对象。我们只需要实例化对象一次，并且也不需要知道它是被哪个线程实例化。虽然所有的线程都能访问到这个ThreadLocal实例，但是每个线程却只能访问到自己通过调用ThreadLocal的set()方法设置的值。即使是两个不同的线程在同一个ThreadLocal对象上设置了不同的值，他们仍然无法访问到对方的值。

如何访问ThreadLocal变量

一旦创建了一个ThreadLocal变量，你可以通过如下代码设置某个需要保存的值：

myThreadLocal.set("A thread local value”);复制代码

可以通过下面方法读取保存在ThreadLocal变量中的值：

String threadLocalValue = (String) myThreadLocal.get();复制代码

get()方法返回一个Object对象，set()对象需要传入一个Object类型的参数。

为ThreadLocal指定泛型类型

public static ThreadLocal<String> myThreadLocal = new ThreadLocal<String>();复制代码

我们可以创建一个指定泛型类型的ThreadLocal对象，这样我们就不需要每次对使用get()方法返回的值作强制类型转换了。下面展示了指定泛型类型的ThreadLocal例子：

ThreadLocal的设计理念与作用

http://blog.csdn.net/u011860731/article/details/48733073http://blog.csdn.net/u011860731/article/details/48733073)

InheritableThreadLocal

public static ThreadLocal<Integer> threadLocal = new InheritableThreadLocal<Integer>();复制代码

InheritableThreadLocal类是ThreadLocal类的子类。ThreadLocal中每个线程拥有它自己的值，与ThreadLocal不同的是，InheritableThreadLocal允许一个线程以及该线程创建的所有子线程都可以访问它保存的值。

InheritableThreadLocal 原理

Java 多线程：InheritableThreadLocal 实现原理

blog.csdn.net/ni357103403…

### ThreadPool（线程池）用法与优势？

为什么要用线程池:

减少了创建和销毁线程的次数，每个工作线程都可以被重复利用，可执行多个任务。

可以根据系统的承受能力，调整线程池中工作线线程的数目，防止因为消耗过多的内存，而把服务器累趴下(每个线程需要大约1MB内存，线程开的越多，消耗的内存也就越大，最后死机)。

Java里面线程池的顶级接口是Executor，但是严格意义上讲Executor并不是一个线程池，而只是一个执行线程的工具。真正的线程池接口是ExecutorService。

new Thread 缺点

每次new Thread新建对象性能差。

线程缺乏统一管理，可能无限制新建线程，相互之间竞争，及可能占用过多系统资源导致死机或oom。

缺乏更多功能，如定时执行、定期执行、线程中断。

ThreadPool 优点

减少了创建和销毁线程的次数，每个工作线程都可以被重复利用，可执行多个任务

可以根据系统的承受能力，调整线程池中工作线线程的数目，防止因为因为消耗过多的内存，而把服务器累趴下(每个线程需要大约1MB内存，线程开的越多，消耗的内存也就越大，最后死机)

减少在创建和销毁线程上所花的时间以及系统资源的开销

如不使用线程池，有可能造成系统创建大量线程而导致消耗完系统内存

Java提供的四种线程池的好处在于：

重用存在的线程，减少对象创建、销毁的开销，提高性能。

可有效控制最大并发线程数，提高系统资源的使用率，同时避免过多资源竞争，避免堵塞。

提供定时执行、定期执行、单线程、并发数控制等功能。

比较重要的几个类：

| 类                          | 描述                                                         |
| --------------------------- | ------------------------------------------------------------ |
| ExecutorService             | 真正的线程池接口。                                           |
| ScheduledExecutorService    | 能和Timer/TimerTask类似，解决那些需要任务重复执行的问题。    |
| ThreadPoolExecutor          | ExecutorService的默认实现。                                  |
| ScheduledThreadPoolExecutor | 继承ThreadPoolExecutor的ScheduledExecutorService接口实现，周期性任务调度的类实现。 |

要配置一个线程池是比较复杂的，尤其是对于线程池的原理不是很清楚的情况下，很有可能配置的线程池不是较优的，因此在Executors类里面提供了一些静态工厂，生成一些常用的线程池。

Executors提供四种线程池

newCachedThreadPool创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。

newFixedThreadPool 创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。

newScheduledThreadPool 创建一个定长线程池，支持定时及周期性任务执行。

newSingleThreadExecutor 创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。

一般都不用Executors提供的线程创建方式

使用ThreadPoolExecutor创建线程池

ThreadPoolExecutor的构造函数

public ThreadPoolExecutor(int corePoolSize,

​                              int maximumPoolSize,

​                              long keepAliveTime,

​                              TimeUnit unit,

​                              BlockingQueue<Runnable> workQueue,

​                              ThreadFactory threadFactory,

​                              RejectedExecutionHandler handler) {

​        if (corePoolSize < 0 ||

​            maximumPoolSize <= 0 ||

​            maximumPoolSize < corePoolSize ||

​            keepAliveTime < 0)

​            throw new IllegalArgumentException();

​        if (workQueue == null || threadFactory == null || handler == null)

​            throw new NullPointerException();

​        this.corePoolSize = corePoolSize;

​        this.maximumPoolSize = maximumPoolSize;

​        this.workQueue = workQueue;

​        this.keepAliveTime = unit.toNanos(keepAliveTime);

​        this.threadFactory = threadFactory;

​        this.handler = handler;

​    }复制代码

参数：

corePoolSize核心线程数大小，当线程数<corePoolSize ，会创建线程执行runnable

maximumPoolSize 最大线程数， 当线程数 >= corePoolSize的时候，会把runnable放入workQueue中

keepAliveTime 保持存活时间，当线程数大于corePoolSize的空闲线程能保持的最大时间。

unit 时间单位

workQueue 保存任务的阻塞队列

threadFactory 创建线程的工厂

handler 拒绝策略

任务执行顺序：

当线程数小于corePoolSize时，创建线程执行任务。

当线程数大于等于corePoolSize并且workQueue没有满时，放入workQueue中

线程数大于等于corePoolSize并且当workQueue满时，新任务新建线程运行，线程总数要小于maximumPoolSize

当线程总数等于maximumPoolSize并且workQueue满了的时候执行handler的rejectedExecution。也就是拒绝策略。

ThreadPoolExecutor默认有四个拒绝策略：

ThreadPoolExecutor.AbortPolicy() 直接抛出异常RejectedExecutionException

ThreadPoolExecutor.CallerRunsPolicy() 直接调用run方法并且阻塞执行

ThreadPoolExecutor.DiscardPolicy() 直接丢弃后来的任务

ThreadPoolExecutor.DiscardOldestPolicy() 丢弃在队列中队首的任务

当然可以自己继承 RejectedExecutionHandler 来写拒绝策略.

java 四种线程池的使用

juejin.im/post/59df0c…

Concurrent包里的其他东西：ArrayBlockingQueue、CountDownLatch等等。

阻塞队列

1、ArrayBlockingQueue 数组结构组成的有界阻塞队列。

此队列按照先进先出（FIFO）的原则对元素进行排序，但是默认情况下不保证线程公平的访问队列，即如果队列满了，那么被阻塞在外面的线程对队列访问的顺序是不能保证线程公平（即先阻塞，先插入）的。

CountDownLatch

CountDownLatch 允许一个或多个线程等待其他线程完成操作。

应用场景

假如有这样一个需求，当我们需要解析一个Excel里多个sheet的数据时，可以考虑使用多线程，每个线程解析一个sheet里的数据，等到所有的sheet都解析完之后，程序需要提示解析完成。

在这个需求中，要实现主线程等待所有线程完成sheet的解析操作，最简单的做法是使用join。代码如下：

public class JoinCountDownLatchTest {

 

​	public static void main(String[] args) throws InterruptedException {

​		Thread parser1 = new Thread(new Runnable() {

​			@Override

​			public void run() {

​			}

​		});

 

​		Thread parser2 = new Thread(new Runnable() {

​			@Override

​			public void run() {

​				System.out.println("parser2 finish");

​			}

​		});

 

​		parser1.start();

​		parser2.start();

​		parser1.join();

​		parser2.join();

​		System.out.println("all parser finish");

​	}

 

}复制代码

join用于让当前执行线程等待join线程执行结束。其实现原理是不停检查join线程是否存活，如果join线程存活则让当前线程永远wait，代码片段如下，wait(0)表示永远等待下去。

while (isAlive()) {

 wait(0);

}复制代码

方法isAlive()功能是判断当前线程是否处于活动状态。

活动状态就是线程启动且尚未终止，比如正在运行或准备开始运行。

CountDownLatch用法

public class Test {

​     public static void main(String[] args) {   

​	 

​         final CountDownLatch latch = new CountDownLatch(2);

 

​         new Thread(){

​             public void run() {

​                 try {

​                     System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");

​                    Thread.sleep(3000);

​                    System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");

​                    latch.countDown();

​                } catch (InterruptedException e) {

​                    e.printStackTrace();

​                }

​             };

​         }.start();

 

​         new Thread(){

​             public void run() {

​                 try {

​                     System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");

​                     Thread.sleep(3000);

​                     System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");

​                     latch.countDown();

​                } catch (InterruptedException e) {

​                    e.printStackTrace();

​                }

​             };

​         }.start();

 

​         try {

​             System.out.println("等待2个子线程执行完毕...");

​            latch.await();

​            System.out.println("2个子线程已经执行完毕");

​            System.out.println("继续执行主线程");

​        } catch (InterruptedException e) {

​            e.printStackTrace();

​        }

​     }

 }复制代码

线程Thread-0正在执行

线程Thread-1正在执行

等待2个子线程执行完毕...

线程Thread-0执行完毕

线程Thread-1执行完毕

2个子线程已经执行完毕

继续执行主线程复制代码

new CountDownLatch(2)的构造函数接收一个int类型的参数作为计数器，如果你想等待N个点完成，这里就传入N。

当我们调用一次CountDownLatch的countDown()方法时，N就会减1，CountDownLatch的await()会阻塞当前线程，直到N变成零。由于countDown方法可以用在任何地方，所以这里说的N个点，可以是N个线程，也可以是1个线程里的N个执行步骤。用在多个线程时，你只需要把这个CountDownLatch的引用传递到线程里。

Java并发编程：CountDownLatch、CyclicBarrier和 Semaphore

www.importnew.com/21889.html

### synchronized和ReentrantLock的区别？

java在编写多线程程序时，为了保证线程安全，需要对数据同步，经常用到两种同步方式就是Synchronized和重入锁ReentrantLock。

基础知识

可重入锁。可重入锁是指同一个线程可以多次获取同一把锁。ReentrantLock和synchronized都是可重入锁。

可中断锁。可中断锁是指线程尝试获取锁的过程中，是否可以响应中断。synchronized是不可中断锁，而ReentrantLock则提供了中断功能。

公平锁与非公平锁。公平锁是指多个线程同时尝试获取同一把锁时，获取锁的顺序按照线程达到的顺序，而非公平锁则允许线程“插队”。synchronized是非公平锁，而ReentrantLock的默认实现是非公平锁，但是也可以设置为公平锁。

CAS操作(CompareAndSwap)。CAS操作简单的说就是比较并交换。CAS 操作包含三个操作数 —— 内存位置（V）、预期原值（A）和新值(B)。如果内存位置的值与预期原值相匹配，那么处理器会自动将该位置值更新为新值。否则，处理器不做任何操作。无论哪种情况，它都会在 CAS 指令之前返回该位置的值。CAS 有效地说明了“我认为位置 V 应该包含值 A；如果包含该值，则将 B 放到这个位置；否则，不要更改该位置，只告诉我这个位置现在的值即可。”

Synchronized

synchronized是java内置的关键字，它提供了一种独占的加锁方式。synchronized的获取和释放锁由JVM实现，用户不需要显示的释放锁，非常方便。然而synchronized也有一定的局限性

例如：

当线程尝试获取锁的时候，如果获取不到锁会一直阻塞。

如果获取锁的线程进入休眠或者阻塞，除非当前线程异常，否则其他线程尝试获取锁必须一直等待。

ReentrantLock

ReentrantLock它是JDK 1.5之后提供的API层面的互斥锁，需要lock()和unlock()方法配合try/finally语句块来完成。

代码示例

private Lock lock = new ReentrantLock();public void test(){

 lock.lock();

 try{

 doSomeThing();

 }catch (Exception e){

 // ignored

 }finally {

 lock.unlock();

 }

}复制代码

lock(), 如果获取了锁立即返回，如果别的线程持有锁，当前线程则一直处于休眠状态，直到获取锁

tryLock(), 如果获取了锁立即返回true，如果别的线程正持有锁，立即返回false；

tryLock(long timeout,TimeUnit unit)，如果获取了锁定立即返回true，如果别的线程正持有锁，会等待参数给定的时间，在等待的过程中，如果获取了锁定，就返回true，如果等待超时，返回false；

lockInterruptibly:如果获取了锁定立即返回，如果没有获取锁定，当前线程处于休眠状态，直到或者锁定，或者当前线程被别的线程中断

ReentrantLock 一些特性

等待可中断避免，出现死锁的情况（如果别的线程正持有锁，会等待参数给定的时间，在等待的过程中，如果获取了锁定，就返回true，如果等待超时，返回false）

公平锁与非公平锁多个线程等待同一个锁时，必须按照申请锁的时间顺序获得锁，Synchronized锁非公平锁，ReentrantLock默认的构造函数是创建的非公平锁，可以通过参数true设为公平锁，但公平锁表现的性能不是很好。

公平锁：线程获取锁的顺序和调用lock的顺序一样，FIFO；

非公平锁：线程获取锁的顺序和调用lock的顺序无关，全凭运气。

Java并发包(java.util.concurrent)中大量使用了CAS操作,涉及到并发的地方都调用了sun.misc.Unsafe类方法进行CAS操作。

ReenTrantLock实现的原理：

简单来说，ReenTrantLock的实现是一种自旋锁，通过循环调用CAS操作来实现加锁。它的性能比较好也是因为避免了使线程进入内核态的阻塞状态。想尽办法避免线程进入内核的阻塞状态是我们去分析和理解锁设计的关键钥匙。

总结一下

在Synchronized优化以前，synchronized的性能是比ReenTrantLock差很多的，但是自从Synchronized引入了偏向锁，轻量级锁（自旋锁）后，两者的性能就差不多了，在两种方法都可用的情况下，官方甚至建议使用synchronized，其实synchronized的优化我感觉就借鉴了ReenTrantLock中的CAS技术。都是试图在用户态就把加锁问题解决，避免进入内核态的线程阻塞。

synchronized：

在资源竞争不是很激烈的情况下，偶尔会有同步的情形下，synchronized是很合适的。原因在于，编译程序通常会尽可能的进行优化synchronize，另外可读性非常好。

ReentrantLock:

ReentrantLock用起来会复杂一些。在基本的加锁和解锁上，两者是一样的，所以无特殊情况下，推荐使用synchronized。ReentrantLock的优势在于它更灵活、更强大，增加了轮训、超时、中断等高级功能。

ReentrantLock默认使用非公平锁是基于性能考虑，公平锁为了保证线程规规矩矩地排队，需要增加阻塞和唤醒的时间开销。如果直接插队获取非公平锁，跳过了对队列的处理，速度会更快。

ReentrantLock实现原理

www.cnblogs.com/maypattis/p…

分析ReentrantLock的实现原理(ReentrantLock和同步工具类的实现基础都是AQS)

www.jianshu.com/p/fe027772e…

### Semaphore有什么作用？

Semaphore就是一个信号量，它的作用是限制某段代码块的并发数。

Semaphore有一个构造函数，可以传入一个int型整数n，表示某段代码最多只有n个线程可以访问，

如果超出了n，那么请等待，等到某个线程执行完毕这段代码块，下一个线程再进入。

由此可以看出如果Semaphore构造函数中传入的int型整数n=1，相当于变成了一个synchronized了。

Semaphore类位于java.util.concurrent包下，它提供了2个构造器：

//参数permits表示许可数目，即同时可以允许多少线程进行访问  public Semaphore(int permits) {  

​    sync = new NonfairSync(permits);  

}  //这个多了一个参数fair表示是否是公平的，即等待时间越久的越先获取许可  public Semaphore(int permits, boolean fair) {  

​    sync = (fair)? new FairSync(permits) : new NonfairSync(permits);  

}  复制代码

Semaphore类中比较重要的几个方法，首先是acquire()、release()方法：

acquire()用来获取一个许可，若无许可能够获得，则会一直等待，直到获得许可。

release()用来释放许可。注意，在释放许可之前，必须先获获得许可。

Semaphore类中比较重要的几个方法，首先是acquire()、release()方法：

acquire()用来获取一个许可，若无许可能够获得，则会一直等待，直到获得许可。

release()用来释放许可。注意，在释放许可之前，必须先获获得许可。复制代码

这4个方法都会被阻塞，如果想立即得到执行结果，可以使用下面几个方法：

//尝试获取一个许可，若获取成功，则立即返回true，若获取失败，则立即返回false  public boolean tryAcquire() { };  //尝试获取一个许可，若在指定的时间内获取成功，则立即返回true，否则则立即返回false  public boolean tryAcquire(long timeout, TimeUnit unit) throws InterruptedException { };   //尝试获取permits个许可，若获取成功，则立即返回true，若获取失败，则立即返回false  public boolean tryAcquire(int permits) { };   //尝试获取permits个许可，若在指定的时间内获取成功，则立即返回true  public boolean tryAcquire(int permits, long timeout, TimeUnit unit) throws InterruptedException { };  //得到当前可用的许可数目  public int availablePermits(); 复制代码

示例

假若一个工厂有5台机器，但是有8个工人，一台机器同时只能被一个工人使用，只有使用完了，其他工人才能继续使用。那么我们就可以通过Semaphore来实现：

public class Test {  

​    public static void main(String[] args) {  

​        int N = 8; //工人数  

​        Semaphore semaphore = new Semaphore(5); //机器数目  

​        for(int i=0;i<N;i++)  

​            new Worker(i,semaphore).start();  

​    }      

​    static class Worker extends Thread{  

​        private int num;  

​        private Semaphore semaphore;  

​        public Worker(int num,Semaphore semaphore){  

​            this.num = num;  

​            this.semaphore = semaphore;  

​        }          

​        @Override  

​        public void run() {  

​            try {  

​                semaphore.acquire();  

​                System.out.println("工人"+this.num+"占用一个机器在生产...");  

​                Thread.sleep(2000);  

​                System.out.println("工人"+this.num+"释放出机器");  

​                semaphore.release();              

​            } catch (InterruptedException e) {  

​                e.printStackTrace();  

​            }  

​        }  

​    }  

} 复制代码

运行结果：

工人0占用一个机器在生产...  

工人1占用一个机器在生产...  

工人2占用一个机器在生产...  

工人4占用一个机器在生产...  

工人5占用一个机器在生产...  

工人0释放出机器  

工人2释放出机器  

工人3占用一个机器在生产...  

工人7占用一个机器在生产...  

工人4释放出机器  

工人5释放出机器  

工人1释放出机器  

工人6占用一个机器在生产...  

工人3释放出机器  

工人7释放出机器  

工人6释放出机器复制代码

### Java Concurrency API中的Lock接口(Lock interface)是什么？对比同步它有什么优势？

Lock接口比同步方法和同步块提供了更具扩展性的锁操作。他们允许更灵活的结构，可以具有完全不同的性质，并且可以支持多个相关类的条件对象。

它的优势有：

可以使锁更公平

可以使线程在等待锁的时候响应中断

可以让线程尝试获取锁，并在无法获取锁的时候立即返回或者等待一段时间

可以在不同的范围，以不同的顺序获取和释放锁

### Hashtable的size()方法中明明只有一条语句”return count”，为什么还要做同步？

同一时间只能有一条线程执行固定类的同步方法，但是对于类的非同步方法，可以多条线程同时访问。所以，这样就有问题了，可能线程A在执行Hashtable的put方法添加数据，线程B则可以正常调用size()方法读取Hashtable中当前元素的个数，那读取到的值可能不是最新的，可能线程A添加了完了数据，但是没有对size++，线程B就已经读取size了，那么对于线程B来说读取到的size一定是不准确的。

而给size()方法加了同步之后，意味着线程B调用size()方法只有在线程A调用put方法完毕之后才可以调用，这样就保证了线程安全性

### ConcurrentHashMap的并发度是什么？

ConcurrentHashMap的并发度就是segment的大小，默认为16，这意味着最多同时可以有16条线程操作ConcurrentHashMap，这也是ConcurrentHashMap对Hashtable的最大优势

### ReentrantReadWriteLock读写锁的使用

Lock比传统线程模型中的synchronized方式更加面向对象，与生活中的锁类似，锁本身也应该是一个对象。两个线程执行的代码片段要实现同步互斥的效果，它们必须用同一个Lock对象。

读写锁：分为读锁和写锁，多个读锁不互斥，读锁与写锁互斥，这是由jvm自己控制的，你只要上好相应的锁即可。 如果你的代码只读数据，可以很多人同时读，但不能同时写，那就上读锁；

如果你的代码修改数据，只能有一个人在写，且不能同时读取，那就上写锁。总之，读的时候上读锁，写的时候上写锁！

ReentrantReadWriteLock会使用两把锁来解决问题，一个读锁，一个写锁

线程进入读锁的前提条件：

没有其他线程的写锁

没有写请求或者有写请求，但调用线程和持有锁的线程是同一个

线程进入写锁的前提条件：

没有其他线程的读锁

没有其他线程的写锁

读锁的重入是允许多个申请读操作的线程的，而写锁同时只允许单个线程占有，该线程的写操作可以重入。

如果一个线程占有了写锁，在不释放写锁的情况下，它还能占有读锁，即写锁降级为读锁。

对于同时占有读锁和写锁的线程，如果完全释放了写锁，那么它就完全转换成了读锁，以后的写操作无法重入，在写锁未完全释放时写操作是可以重入的。

公平模式下无论读锁还是写锁的申请都必须按照AQS锁等待队列先进先出的顺序。非公平模式下读操作插队的条件是锁等待队列head节点后的下一个节点是SHARED型节点，写锁则无条件插队。

读锁不允许newConditon获取Condition接口，而写锁的newCondition接口实现方法同ReentrantLock。