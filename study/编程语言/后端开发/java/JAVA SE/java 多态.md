多态是同一个行为具有多个不同表现形式或形态的能力。多态就是同一个接口，使用不同的实例而执行不同操作。

多态性是对象多种表现形式的体现，比如：

在现实中，我们按下F1键这个动作：

* 如果当前在Flash界面下弹出的就是AS 3的帮助文档
* 如果当前在Word下弹出的就是Word帮助
* 在Windows下弹出的就是Windows帮助和支持

#### 多态存在的三个必要条件

* 继承
* 重写
* 父类引用指向子类对象

```
Parent p = new Child();
```

当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法。

#### 相关例题

```
1. 问这个程序的输出结果。(D)
    package Wangyi;
    class Base
    {
        public void method()
        {
            System.out.println("Base");
        } 
    }
    class Son extends Base
    {
        public void method()
        {
            System.out.println("Son");
        }

        public void methodB()
        {
            System.out.println("SonB");
        }
    }
    public class Test01
    {
        public static void main(String[] args)
        {
            Base base = new Son();
            base.method();
            base.methodB();
        }
    }
    A. Base SonB
    B. Son SonB
    C. Base Son SonB
    D.编译不通过
    解释：
    Base base=new Son(); 是多态的表示形式。父类对象调用了子类创建了Son对象。
    base调用的method()方法就是调用了子类重写的method()方法。
    而此时base还是属于Base对象，base调用methodB()时Base对象里没有这个方法，所以编译不通过。
    要想调用的话需要先通过SON son=(SON)base;强制转换，然后用son.methodB()调用。
2. 判断对错，在java的多态调用中，new的是哪一个类就是调用的哪个类的方法。（B）
    A. 对
    B. 错
    解析：这个应该分情况的：
    	普通方法，运用的是动态单分配，根据new的类型确定对象，从而确定调用的方法，
    	静态方法，运用的是静态多分配，根据静态类型确定对象。
    	例子：
		public class Father { 
            public void say(){ 
                System.out.println("father"); 
            } 
            public static void action(){ 
                System.out.println("爸爸打儿子！"); 
            } 
        } 
        public class Son extends Father{ 
            public void say() { 
                System.out.println("son"); 
            }
           public static void action(){ 
                System.out.println("打打！"); 
            }
            public static void main(String[] args) { 
                Father f=new Son(); 
                f.say(); 
                f.action(); 
            } 
        }
        输出：
        	son
        	爸爸打儿子！
```

