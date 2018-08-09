关于HashMap你需要了解的：

```
1. HashMap的实例有两个参数影响其性能：“初始容量”和“加载因子”。
2. HashMap的实现是不同步的，线程不是安全的。
3. HashMap采用拉链法解决哈希冲突的
4. HashMap中的key-value都是存储在Entry数组中。
5. HashMap中key不能重复，value可以重复
6. HashMap是无序的
7. HashMap中key-value都允许为空，但只允许其中一个为空
```

#### 相关面试题

##### 1. 下面有关java hashmap的说法错误的是？( )

```
A. HashMap 的实例有两个参数影响其性能：“初始容量” 和 “加载因子”。
B. HashMap 的实现不是同步的，意味着它不是线程安全的
C. HashMap通过开放地址法解决哈希冲突
D. HashMap中的key-value都是存储在Entry数组中的
```

```
解析：答案：C
  	HashMap 采用拉链法解决冲突
```

##### 2. 关于HashMap与HashTable，以下说法错误的是 （ )

```
A. 两者都是用key-value方式获取数据
B. Hashtable允许null值作为key和value，而HashMap不可以
C. HashMap不是同步的，而Hashtable是同步的
D. 迭代HashMap采用快速失败机制，而Hashtable不是
```

```
 解析：答案：B
  	HashTable不允许null值(key和value都不可以),HashMap允许null值(key和value都可以)
  	Hashtable的方法是Synchronize的，而HashMap不是，
  	在多个线程访问Hashtable时，不需要自己为它的方法实现同步，
  	而HashMap 就必须为之提供外同步。
```

##### 3. 有关hashMap跟hashTable的区别，说法正确的是？（ ）

```
A. HashMap和Hashtable都实现了Map接口
B. HashMap是非synchronized，而Hashtable是synchronized
C. HashTable使用Enumeration，HashMap使用Iterator
D. Hashtable直接使用对象的hashCode，HashMap重新计算hash值，而且用与代替求模

解析：答案：A,B,C,D
```

#####  4. HashMap和HashTable的描述，错误的是？

```
A. 他们都实现了Map接口。
B. HashMap非线程安全，在多个线程访问Hashtable时，
	不需要自己为它的方法实现同步，而HashMap就必须为之提供额外同步。
C. HashMap允许将null作为一个entry的key或者value，而Hashtable不允许。
D. 通过contains方法可以判断一个对象是否存在于HashMap或者Hashtable中。

解析：
	HashMap中没有contain方法。
```

##### 5. 在Java中，关于HashMap类的描述，以下错误的是（）？

```
A. HashMap能够保证其中元素的顺序
B. HashMap允许将null用作值
C. HashMap允许将null用作键
D. HashMap使用键/值得形式保存数据

解析：答案：A
    HashMap是无序的
    HashMap允许Key/Value值都为null
```

支持我的话可以关注下我的微信公众号，每天都会推送新知识~

> ![](C:\Users\ttxxl\Pictures\20180404220912740.jpg)![](C:\Users\ttxxl\Pictures\qrcode_for_gh_e125acf2ab2b_258.jpg)

发表于：

* https://blog.csdn.net/jdliyao/article/details/79837119
* 微信公众号 - darklovy
* https://juejin.im/post/5b568aed51882506e232b5bf