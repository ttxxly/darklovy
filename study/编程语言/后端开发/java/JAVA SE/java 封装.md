在面向对象程序设计方法中，封装（Encapsulation）是指一种将抽象性函式接口的实现细节部分包装‘隐藏起来的方法。数据被保护在内部，隐藏内部实现细节，对外提供接口与外部交互。

## 实例

让我们来看一个java封装类的例子：

```
/* 文件名: EncapTest.java */
public class EncapTest{
 
   private String name;
   private String idNum;
   private int age;
 
   public int getAge(){
      return age;
   }
 
   public String getName(){
      return name;
   }
 
   public String getIdNum(){
      return idNum;
   }
 
   public void setAge( int newAge){
      age = newAge;
   }
 
   public void setName(String newName){
      name = newName;
   }
 
   public void setIdNum( String newId){
      idNum = newId;
   }
}
```

以上实例中public方法是外部类访问该类成员变量的入口。

通常情况下，这些方法被称为getter和setter方法。

因此，任何要访问类中私有成员变量的类都要通过这些getter和setter方法。

通过如下的例子说明EncapTest类的变量怎样被访问：

```
/* F文件名 : RunEncap.java */
public class RunEncap{
   public static void main(String args[]){
      EncapTest encap = new EncapTest();
      encap.setName("James");
      encap.setAge(20);
      encap.setIdNum("12343ms");
 
      System.out.print("Name : " + encap.getName()+ 
                             " Age : "+ encap.getAge());
    }
}
```

以上代码编译运行结果如下:

```
Name : James Age : 20
```

#### 使用封装的好处

1、良好的封装能够减少耦合

2、类内部的结构可以自由修改。

3、可以对成员进行更精确的控制。

4、隐藏信息，实现细节

#### 参考资料

* http://www.runoob.com/java/java-encapsulation.html
* http://blog.csdn.net/chenssy/article/details/12757911
* https://baike.baidu.com/item/java%20%E7%9A%84%E5%B0%81%E8%A3%85/3388478?fr=aladdin