继承是java面向对象编程技术的一块基石，因为它允许创建分等级层次的类。

继承是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为，也就是常说的 is-a 关系。

#### 类的继承格式

在 Java 中通过 extends 关键字可以申明一个类是从另外一个类继承而来的，一般形式如下：

```
class 父类 {
}
 
class 子类 extends 父类 {
}
```

#### 继承的特性

```
- 子类拥有父类非private的属性，方法。
- 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。
- 子类可以用自己的方式实现父类的方法。
- Java的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如A类继承B类，B类继承C类，所以按照关系就是C类是B类的父类，B类是A类的父类，这是java继承区别于C++继承的一个特性。
- JAVA不支持多继承，单继承使JAVA的继承关系很简单，一个类只能有一个父类，易于管理程序，同时一个类可以实现多个接口，从而克服单继承的缺点。
- 提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系）。
```

#### 继承关键字

继承可以使用 extends 和 implements 这两个关键字来实现继承，而且所有的类都是继承于 java.lang.Object，当一个类没有继承的两个关键字，则默认继承object（这个类在 **java.lang** 包中，所以不需要 **import**）祖先类。

#### extends关键字

在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。

```
public class Animal { 
    private String name;   
    private int id; 
    public Animal(String myName, String myid) { 
        //初始化属性值
    } 
    public void eat() {  //吃东西方法的具体实现  } 
    public void sleep() { //睡觉方法的具体实现  } 
} 
 
public class Penguin  extends  Animal{ 
}
```

#### implements关键字

使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

```
public interface A {
    public void eat();
    public void sleep();
}
 
public interface B {
    public void show();
}
 
public class C implements A,B {
}
```

### super 与 this 关键字

super关键字：我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类。

this关键字：指向自己的引用。

## 实例

```
class Animal {
  void eat() {
    System.out.println("animal : eat");
  }
}
 
class Dog extends Animal {
  void eat() {
    System.out.println("dog : eat");
  }
  void eatTest() {
    this.eat();   // this 调用自己的方法
    super.eat();  // super 调用父类方法
  }
}
 
public class Test {
  public static void main(String[] args) {
    Animal a = new Animal();
    a.eat();
    Dog d = new Dog();
    d.eatTest();
  }
}
```

输出结果为：

```
animal : eat
dog : eat
animal : eat
```

### final关键字

final 关键字声明类可以把类定义为不能继承的，即最终类；或者用于修饰方法，该方法不能被子类重写：

- 声明类：

  ```
  final class 类名 {//类体}
  ```

- 声明方法：

  ```
  修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}
  ```

**注**:实例变量也可以被定义为 final，被定义为 final 的变量不能被修改。被声明为 final 类的方法自动地声明为 final，但是实例变量并不是 final

## 构造器

子类不能继承父类的构造器（构造方法或者构造函数），但是父类的构造器带有参数的，则必须在子类的构造器中显式地通过super关键字调用父类的构造器并配以适当的参数列表。

如果父类有无参构造器，则在子类的构造器中用super调用父类构造器不是必须的，如果没有使用super关键字，系统会自动调用父类的无参构造器。

## 实例

```
class SuperClass {
  private int n;
  SuperClass(){
    System.out.println("SuperClass()");
  }
  SuperClass(int n) {
    System.out.println("SuperClass(int n)");
    this.n = n;
  }
}
class SubClass extends SuperClass{
  private int n;
  
  SubClass(){
    super(300);
    System.out.println("SubClass");
  }  
  
  public SubClass(int n){
    System.out.println("SubClass(int n):"+n);
    this.n = n;
  }
}
public class TestSuperSub{
  public static void main (String args[]){
    SubClass sc = new SubClass();
    SubClass sc2 = new SubClass(200); 
  }
}
```

输出结果为：

```
SuperClass(int n)
SubClass
SuperClass()
SubClass(int n):200
```

#### 相关面试题

```
1. 类B从类A派生，则类B可以访问类A中的（A, C ）成员？
  A. public成员
  B. private成员
  C. protected成员
  D. 所有数据成员
  E. 所有函数成员
  解析：派生类也就是子类，说明两者是继承关系。
  		A. public：当前类，同包，子类，不同包都可以访问
  		B. private：只有当前类才能够访问
  		C. protected：当前类，同包，子类可以访问
  		D. 所有数据成员：A,B不一定同包
  		E. 所有函数成员：A,B不一定同包
 
2. A 派生出子类 B ， B 派生出子类 C ，并且在 Java 源代码中有如下声明：
      1. A  a0=new  A();
      2. A  a1 =new  B();
      3. A  a2=new  C();
问以下哪个说法是正确的？ （ D ）
    A. 只有第1行能通过编译
    B. 第1、2行能通过编译，但第3行编译出错
    C.第1、2、3行能通过编译，但第2、3行运行时出错
    D. 第1行、第2行和第3行的声明都是正确的
    解析：继承具有传递性，子类可以无条件向上转型！
 3. 下列关于继承的描述正确的是（C）
    A. 在Java中允许定义一个子类的引用，指向父类的对象。
    B. 在Java中一个子类可以继承多个抽象类，在extends关键字后依次列出，用逗号隔开。
    C. 在Java中继承是通过extends关键字来描述的，而且只允许继承自一个直接父类。
    D. 在Java中抽象类之间不允许出现继承关系，所有的抽象类都相互独立。
    解析：
    	A. 这个应该不安全的吧，强制转换？instanceof  ？
    	B. 可以实现多个抽象类，只能继承一个直接父类。
    	C. 。。
    	D. 抽象类也是可以继承的。
 4. 关于继承和实现说法正确的是（A）
     A. 类可以实现多个接口，接口可以继承（或扩展）多个接口
     B. 类可以实现多个接口，接口不能继承（或扩展）多个接口
     C. 类和接口都可以实现多个接口
     D. 类和接口都不可以实现多个接口
     解析：
     	类->类：单继承，可以多层继承
     	类->接口：实现，单实现、多实现都可以
     	接口->接口：继承，单继承、多继承都可以
 5. 代码的运行结果是（C）
    package com.sunline.java;
    public class A implements B extends C{
        public static void main(String args[]){
            System.out.println("hello sunline!");
        }
    }
    A. 在控制台打印hello sunline！
    B. 报异常java.lang.NullPoninterException
    C. 编译报错
    D. 报异常java.lang.RuntimeExcception
    解析：
    	注意语法：先继承再实现
```

