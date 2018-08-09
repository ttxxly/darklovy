Java接口是一系列方法的声明，是一些方法特征的集合，一个接口只有方法的特征没有方法的实现，因此这些方法可以在不同的地方被不同的类实现，而这些实现可以具有不同的行为（功能）。 

```
1. 接口的声明
2. 接口的特性
3. 抽象类和接口的区别
4. 相关面试题
```

#### 接口的声明

```
修饰符 interface 接口名称 [extends 类名称] {
   //声明变量和方法
}
```

#### 接口的特性

```
1. 隐喻抽象
	接口中方法: 隐式的指定为 public abstract（private报错）
	接口中变量：隐式的指定为 public static final （private修饰报错）
```

#### 相关面试题

```
1. 下面选项中,哪些是interface中合法方法定义?(A,C,D) 
    A public void main(String [] args);
    B private int getSum();
    C boolean setFlag(Boolean [] test);
    D public float get(int x);
2. java8中，忽略内部接口的情况，不能用来修饰interface里的方法的有（ ）
    A. private
    B. public
    C. protected
    D. static
    解析：only public, abstract, default, static and strictfp 
```



#### 接口的意义

1. 规范性：如果一个项目比较庞大，那么就需要一个能理清所有业务的架构师来定义一些主要的接口，这些接口不仅告诉开发人员你需要实现那些业务，而且也将命名规范限制住了（防止一些开发人员随便命名导致别的程序员无法看明白）。
2. 拓展性：比如你要做一个画板程序，其中里面有一个面板类，主要负责绘画功能，然后你就这样定义了这个类。

   可是在不久将来，你突然发现这个类满足不了你了，然后你又要重新设计这个类，更糟糕是你可能要放弃这个类，那么其他地方可能有引用他，这样修改起来很麻烦。

​         如果你一开始定义一个接口，把绘制功能放在接口里，然后定义类时实现这个接口，然后你只要用这个接口去引用实现它的类就行了，以后要换的话只不过是引用另一个类而已，这样就达到维护、拓展的方便性。

3. 安全、严密性：接口是实现软件松耦合的重要手段，它描叙了系统对外的所有服务，而不涉及任何具体的实现细节。这样就比较安全、严密一些（一般软件服务商考虑的比较多）。
4. 回调：如果遇到一些耗时任务（如网络请求，文件读写，数据库读写等等），我们会将其放入子线程中去执行，当执行完毕后，子线程再将执行结果返回给主线程。




### JDK8及以后，允许我们在接口中定义static方法和default方法。

### 在jdk8之前，interface之中可以定义变量和方法，变量必须是public、static、final的，方法必须是public、abstract的。由于这些修饰符都是默认的，所以在JDK8之前，下面的写法都是等价的.

```
public interface JDK8BeforeInterface {  
    public static final int field1 = 0;  

    int field2 = 0;  

    public abstract void method1(int a) throws Exception;  

    void method2(int a) throws Exception;  
}

```

### JDK8及以后，允许我们在接口中定义static方法和default方法。

```
public interface JDK8Interface {  

    // static修饰符定义静态方法  
    static void staticMethod() {  
        System.out.println("接口中的静态方法");  
    }  

    // default修饰符定义默认方法  
    default void defaultMethod() {  
        System.out.println("接口中的默认方法");  
    }  
}

```

再定义一个接口的实现类：

```
public class JDK8InterfaceImpl implements JDK8Interface {  
    //实现接口后，因为默认方法不是抽象方法，所以可以不重写，但是如果开发需要，也可以重写  
}

```

### 静态方法，只能通过接口名调用，不可以通过实现类的类名或者实现类的对象调用。default方法，只能通过接口实现类的对象来调用。

```
public class Main {  
    public static void main(String[] args) {  
        // static方法必须通过接口类调用  
        JDK8Interface.staticMethod();  

        //default方法必须通过实现类的对象调用  
        new JDK8InterfaceImpl().defaultMethod();  
    }  
}

```

### 当然如果接口中的默认方法不能满足某个实现类需要，那么实现类可以覆盖默认方法。

```
public class AnotherJDK8InterfaceImpl implements JDK8Interface {  

    // 签名跟接口default方法一致,但是不能再加default修饰符  
    @Override  
    public void defaultMethod() {  
        System.out.println("接口实现类覆盖了接口中的default");  
    }  
}

```

由于java支持一个实现类可以实现多个接口，如果多个接口中存在同样的static和default方法会怎么样呢？如果有两个接口中的静态方法一模一样，并且一个实现类同时实现了这两个接口，此时并不会产生错误，因为jdk8只能通过接口类调用接口中的静态方法，所以对编译器来说是可以区分的。但是如果两个接口中定义了一模一样的默认方法，并且一个实现类同时实现了这两个接口，那么必须在实现类中重写默认方法，否则编译失败。

```
public interface JDK8Interface1 {  

    // static修饰符定义静态方法  
    static void staticMethod() {  
        System.out.println("JDK8Interface1接口中的静态方法");  
    }  

    // default修饰符定义默认方法  
    default void defaultMethod() {  
        System.out.println("JDK8Interface1接口中的默认方法");  
    }  

}

```

```
public class JDK8InterfaceImpl implements JDK8Interface,JDK8Interface1 {  

    // 由于JDK8Interface和JDK8Interface1中default方法一样,所以这里必须覆盖  
    @Override  
    public void defaultMethod() {  
        System.out.println("接口实现类覆盖了接口中的default");  
    }  
}

public class Main {  
    public static void main(String[] args) {  
        JDK8Interface.staticMethod();  
        JDK8Interface1.staticMethod();  
        new JDK8InterfaceImpl().defaultMethod();  
    }  
}

```