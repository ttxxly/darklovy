定义在一个类中或者方法中的类称为内部类.

内部类可以分为：

* 成员内部类
* 局部内部类
* 匿名内部类
* 静态内部类

#### 内部类的共性

1. 内部类仍然是一个独立的类，内部类会被编译成独立的.class 文件，但是在名字前面会加上外部类的类名和$符号
2. 内部类不能用普通的方式访问。内部类是外部类的一个成员，因此内部类可以自由地访问外部类的成员变量，无论是否是private的。
3. 内部类声明成静态的，就不能随便的访问内部类的成员变量了， 此时就只能访问外部类的静态成员变量。

#### 内部类的作用

1. 内部类可以用多个实例，每个实例都有自己的状态信息，并且与其他外围对象的信息相互独立。
2. 在单个外围类中，可以让多个内部类以不同的方式实现同一个接口，或者继承同一个类。
3. 创建内部类对象的时刻并不依赖于外围类对象的创建。
4. 内部类并没有令人迷惑的“is-a”关系，他就是一个独立的实体。
5. 内部类提供了更好的封装，除了该外围类，其他类都不能访问

#### 成员内部类

成员内部类是最普通的内部类，定义在一个类的内部中，如同一个成员变量一样，形式如下：

```
public class OutClass2 {
    private int i = 1;
    public static String str = "outclass";

    class InnerClass { // 成员内部类
        private int i = 2;

        public void innerMethod() {
            int i = 3;
            System.out.println("i=" + i);
            System.out.println("i=" + this.i);
            System.out.println("i=" + OutClass2.this.i);
            System.out.println("str=" + str);
        }
    }
}

public class TestClass {

    public static void main(String[] args) {
        //先创建外部类对象
        OutClass2 outClass = new OutClass2(); 
        //创建内部类对象
        OutClass2.InnerClass in = outClass.new InnerClass();
        //内部类对象调用自己的方法
        in.innerMethod();
    }
} 
```

#### 静态内部类

使用 static 关键字修饰的内部类就是静态类，静态内部类和外部类没有任何关系，可以看做是和外部类平级的类。

```
public class Outclass3 {

    private String name;
    private int age;

    public static class InnerStaticClass {

        private String name;

        public String getName() {
            return name;
        }

        public int getAge() {
            return new Outclass3().age;
        }
    }
}
```

静态内部类很干净，没有持有外部类的引用，我们要访问外部类的成员只能 new 一个外部类的对象。

否则只能访问外部类的**静态属性和静态方法**，同理外部类只能访问内部类的**静态属性和静态方法**。

#### 局部内部类

局部内部类是指在代码块或者方法中创建的类。

它和成员内部类的区别就是：局部内部类的作用域只能在其所在的代码块或者方法内，在其它地方是无法创建该类的对象。

```
public class OutClass4 {
    private String className = "OutClass";

    {
        class PartClassOne { // 局部内部类
            private void method() {
                System.out.println("PartClassOne " + className);
            }
        }
        new PartClassOne().method();
    }

    public void testMethod() {
        class PartClassTwo { // 局部类内部类
            private void method() {
                System.out.println("PartClassTwo " + className);
            }
        }
        new PartClassTwo().method();
    }
}
```

(1)、方法内部类只能在定义该内部类的方法内实例化，不可以在此方法外对其实例化。

(2)、方法内部类对象不能使用该内部类所在方法的非final[局部变量](https://baike.baidu.com/item/%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F)。

因为方法的局部变量位于栈上，只存在于该方法的[生命期](https://baike.baidu.com/item/%E7%94%9F%E5%91%BD%E6%9C%9F)内。当一个方法结束，其栈结构被删除，局部变量成为历史。但是该方法结束之后，在方法内创建的内部类对象可能仍然存在于堆中！例如，如果对它的引用被传递到其他某些代码，并存储在一个[成员变量](https://baike.baidu.com/item/%E6%88%90%E5%91%98%E5%8F%98%E9%87%8F)内。正因为不能保证局部变量的存活期和方法内部类对象的一样长，所以内部类对象不能使用它们。

#### 匿名内部类

顾名思义，没有名字的内部类

`Car jeep=new Car();`

在Java中**操纵的标识符实际是指向一个对象的引用**，也就是说 `jeep` 是一个指向 `Car` 类对象的引用，而右面的 `new Car()` 才是真正创建对象的语句。

这可以将 `jeep` 抽象的理解为 `Car` 类对象的“名字”，而匿名内部类顾名思义可以抽象的理解为没有“名字”的内部类:

> 匿名内部类的特点： 
> 1.一个类用于继承其他类或是实现接口，并不需要增加额外的方法，只是对继承方法的实现或是覆盖。 
> 3.类名没有意义，也就是不需要使用到。

```
button.setOnClickListener(new OnClickListener() {
    @Override
    public void onClick(View v) {
    // TODO Auto-generated method stub
    }
});
```

上面代码是 Android 中最常见的设置 button 的点击事件，其中 `new OnClickListener() {…}` 就是一个匿名内部类，在这里没有创建类对象的引用，而是直接创建的类对象。大部分匿名类用于接口回调。

#### 内部类的意义

1. 内部类可以用多个实例，每个实例都有自己的状态信息，并且与其他外围对象的信息相互独立。
2. 在单个外围类中，可以让多个内部类以不同的方式实现同一个接口，或者继承同一个类。
3. 创建内部类对象的时刻并不依赖于外围类对象的创建。
4. 内部类并没有令人迷惑的“is-a”关系，他就是一个独立的实体。
5. 内部类提供了更好的封装，除了该外围类，其他类都不能访问

#### 相关面试题

```
1. 关于匿名内部类叙述正确的是？ ( B )
  A. 匿名内部类可以继承一个基类，不可以实现一个接口
  B. 匿名内部类不可以定义构造器
  C. 匿名内部类不能用于形参
  D. 以上说法都不正确
  解析：
  	1. 使用匿名内部类时，必须继承一个类或实现一个接口
  	2. 匿名内部类由于没有名字，因此不能定义构造函数
  	3. 匿名内部类中不能含有静态成员变量和静态方法
  	
2. 往OuterClass类的代码段中插入内部类声明, 哪一个是错误的:
    public class OuterClass{
        private float f=1.0f;
        //插入代码到这里
    }
    A. class InnerClass{
    public static float func(){return f;}
    }
    B. abstract class InnerClass{
    public abstract float func(){}
    }
    C. static class InnerClass{
    protected static float func(){return f;}
    }
    D. public class InnerClass{
     static float func(){return f;}
    }
  	解析：
  		静态方法不能访问非静态变量，A、C、D错；
		抽象类中的抽象方法不能有方法体，B错；
```



#### 参考资料

1. [java 基础巩固：内部类的字节码学习和实战使用场景](http://blog.csdn.net/u011240877/article/details/78682097) 
2. [java 提高篇（八)----- 详解内部类](https://www.cnblogs.com/chenssy/p/3388487.html) 
3. [百度百科---java 内部类](https://baike.baidu.com/item/java%E5%86%85%E9%83%A8%E7%B1%BB) 