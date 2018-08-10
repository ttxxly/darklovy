Volatile（易变型变量） 是一个类型修饰符（type specifier），它是被设计用来修饰被不同线程访问和修改的变量。Volatile的作用是作为指令关键字，确保本条指令不会因为编译器的优化而省略，且要求每次直接读值。

#### 作用

防止编译器对代码进行优化。如下程序：

```
XBYTE[2]=0x55;
XBYTE[2]=0x56;
XBYTE[2]=0x57;
XBYTE[2]=0x58;
```

对外部硬件而言，上述语句分别表示不同的操作。会产生四种不同的动作，但是编译器却会对上述四条语句进行优化，认为`XBYTE[2]=0x58;`(忽略前三条语句，只产生一条机器代码)。如果用 volatile 修饰，则编译器会逐一地进行编译并产生相应的机器代码（产生四条代码）。

#### 相关面试题

1. java中能创建 volatile 数组吗？

   能。java中可以创建volatile数组，不过只是一个指向数组的引用，而不是整个数组。如果改变引用指向的数组，将会受到 volatile 的保护，但是如果多个线程同时改变数组的元素，volatile 标示符就不能起到之前的保护作用了。

2. volatile 类型变量提供什么保证？

   volatile 变量提供顺序和可见性保证。例如，JVM 或者 JIT（即时编译）为了获得更好的性能会对语句重排序，但是 volatile 类型变量即使在没有同步块的情况下赋值也不会与其他语句重排序。 volatile 提供 happens-before 的保证，确保一个线程的修改能对其他线程是可见的。某些情况下，volatile 还能提供原子性，如读 64 位数据类型，像 long 和 double 都不是原子的，但 volatile 类型的 double 和 long 就是原子的。

#### 参考

* https://baike.baidu.com/item/volatile
* https://www.ibm.com/developerworks/cn/java/j-jtp06197.html