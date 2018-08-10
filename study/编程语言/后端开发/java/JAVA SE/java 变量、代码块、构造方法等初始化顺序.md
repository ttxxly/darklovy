在java中有普通的成员变量、静态成员变量、静态代码块、构造代码块、子类的构造方法和父类的构造方法等。那么它们的初始化顺序是怎样的呢？

```
1. 初始化父类中的静态成员变量和静态代码块 ； 
2. 初始化子类中的静态成员变量和静态代码块 ； 
3.初始化父类的普通成员变量和代码块，再执行父类的构造方法；
4.初始化子类的普通成员变量和代码块，再执行子类的构造方法； 
```

#### 相关练习题

```
1. 以下程序执行的结果是：（C）
    class X{
        Y y=new Y();
        public X(){
            System.out.print("X");
        }
    }
    class Y{
        public Y(){
            System.out.print("Y");
        }
    }
    public class Z extends X{
        Y y=new Y();链接：https://www.nowcoder.com/questionTerminal/27a89bce14c242d1a4161fbeca2b6b7e
来源：牛客网

1）初始化父类的普通成员变量和代码块，执行  Y y=new Y();  输出Y 
（2）再执行父类的构造方法；输出X
（3） 初始化子类的普通成员变量和代码块，执行  Y y=new   Y();  输出Y 
（4）再执行子类的构造方法；输出Z
        public Z(){
            System.out.print("Z");
        }
        public static void main(String[] args) {
            new Z();
        }
    }
    A. ZYXX
    B. ZYXY
    C. YXYZ
    D. XYZX
    解析：
    （1）初始化父类的普通成员变量和代码块，执行  Y y=new Y();  输出Y 
    （2）再执行父类的构造方法；输出X
    （3） 初始化子类的普通成员变量和代码块，执行  Y y=new   Y();  输出Y 
    （4）再执行子类的构造方法；输出Z
```

