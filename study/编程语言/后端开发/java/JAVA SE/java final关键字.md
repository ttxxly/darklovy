final 是 java 的关键字，适用于数据‘、方法、类。它表示这部分数据是不可变的。

### 1. 修饰类

使用final来修饰的类叫做final类。它们是不能够被继承的。java 中有许多的类都是final类。比如String、Integer以及其他的包装类。final类中的成员变量可以根据需要设为final，但是要注意final类中的所有成员方法偶会被隐式的指定为final方法。

**没有必要尽量不要将类设计为final类，除非这个类不会用来继承或者出于安全的考虑**

#### 2. 修饰方法

方法前面加上final关键字，代表这个方法不可以被子类的方法重写。使用final方法的原因有两个，第一个原因是方法锁定，以防止任何继承类修改它的含义；第二个原因是效率：在早期的Java实现版本中，会将final方法转为内嵌调用。但是如果方法过于庞大，可能看不到内嵌调用带来的任何性能提升。在最近的Java版本中，不需要使用final方法进行这些优化了。“

#### 3. 修饰变量

凡是对成员变量或者本地变量(在方法中的或者代码块中的变量称为本地变量)声明为final的都叫作final变量。对于一个final变量，如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象，但是引用对象的内容是可变的。

### final关键字的好处

1. final关键字提高了性能。JVM和Java应用都会缓存final变量。
2. final变量可以安全的在多线程环境下进行共享，而不需要额外的同步开销。
3. 使用final关键字，JVM会对方法、变量及类进行优化。

#### 相关面试题

```
1. final、finally和finalize的区别中，下述说法正确的有？(A, B)
  A. final用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，类不可继承。
  B. finally是异常处理语句结构的一部分，表示总是执行。
  C. finalize是Object类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，可以覆盖此方法提供垃圾收集时的其他资源的回收，例如关闭文件等。
  D. 引用变量被final修饰之后，不能再指向其他对象，它指向的对象的内容也是不可变的。
  解析：
  	A.不用解析
  	B.一般来说执行完 try catch 之后就会执行 finally，在try catch语句块中使用System.exit(0);finally就不会执行了；
  	C:有一种JNI(Java Native Interface)调用non-Java程序（C或C++），finalize()的工作就是回收这部分的内存。并不是用于关闭文件等， 应该是这里错了
  	D: 对象引用不变，但是指向对象的内容是可变的
  		final StringBuffer sb = new StringBuffer();
		sb.append("hello");
```



#### 参考

* http://www.cnblogs.com/chenssy/p/3428180.html
* http://www.importnew.com/7553.html
* https://www.cnblogs.com/dolphin0520/p/3736238.html