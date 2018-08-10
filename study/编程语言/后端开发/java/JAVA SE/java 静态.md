按照是否静态的对类成员变量进行分类可分两种：一种是被static修饰的变量，叫静态变量或类变量；另一种是没有被static修饰的变量，叫实例变量。两者的区别是：

对于静态变量在内存中只有一个拷贝（节省内存），JVM只为静态分配一次内存，在加载类的过程中完成静态变量的内存分配，可用类名直接访问（方便），当然也可以通过对象来访问（但是这是不推荐的）。

对于实例变量，每创建一个实例，就会为实例变量分配一次内存，实例变量可以在内存中有多个拷贝，互不影响

#### 相关面试题

```
1. 如下的代码的输出结果是什么？（答案：D）
    public class Test {
        public int aMethod(){
            static int i = 0;
            i++;
            return i;
        }
    public static void main(String args[]){
        Test test = new Test();
        test.aMethod();
        int j = test.aMethod();
        System.out.println(j);
        }
    }
    A. 0
    B. 1
    C. 2
    D. 编译失败
    解析：
 2. 对于下面这段代码，以下说法正确的是：（C）
 	public class Test
    {
        public int x;
        public static void main(String []args)
        {
            System. out. println("Value is" + x);
        }
    }
    A. 程序会打出 "Value is 0"
    B. 程序会抛出 NullPointerException
    C. 非静态变量不能够被静态方法引用
    D. 编译器会抛出 "possible reference before assignment"的错误
    解析：
    	非静态成员只能被类的实例化对象引用，因此在静态方法中访问x会编译出错
 3. 假设 A 类有如下定义，设 a 是 A 类同一个包下的一个实例，下列语句调用哪个是错误的？（C）
    class A{
    int  i;
    static  String  s;
    void  method1() {   }
    static  void  method2()  {   }

    }
    A. System.out.println(a.i)；
    B. a.method1();
    C. A.method1();
    D. A.method2()
    解析：只有静态方法才能通过类名来调用，非静态方法要通过对象来调用。
```

