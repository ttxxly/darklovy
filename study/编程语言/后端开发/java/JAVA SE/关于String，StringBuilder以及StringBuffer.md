```
1. 是否可变
	String：不可变对象
		一旦被创建就不能修改它的值
		对已存在String对象的修改都是重新创建一个新的对象
	StringBuffer：可变对象
		通过构造函数建立对象：StringBuffer sb = new StringBuffer();
		不能通过赋值号'='进行赋值
		通过它的append()方法进行赋值： sb.append("hello");
2. 是否线程安全
	String：线程安全
		String 对象不可变的。
	StringBuffer：线程安全
		对方法或者对调用的方法加了同步锁
			public synchronized StringBuffer reverse() {
                super.reverse();  
                return  this ;
			}
              public int indexOf(String str) {
              //存在 public synchronized int indexOf(String str, int fromIndex) 方法
                  return indexOf(str, 0);         
              }
	StringBuilder：线程不安全
		没有对方法加同步锁
```

#### 相关面试题

```
1. StringBuffer类对象创建之后可以在修改和变动（正确）
	解析：
		String对象不可变，对已存在String对象的修改都是重新创建一个新的对象
		StringBuffer对象可变。append()方法
		
```

