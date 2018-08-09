#### 相关面试题

##### 1. 假设有以下代码

```
String s = "hello";
String t = "hello";
char c[] = {'h', 'e', 'l', 'l', 'o'};
```

下列选项中返回false的语句是：()

```
A s.equals(t);
B t.equals(c);
C s==t;
D t.equals(new String ("hello"));
```

```
解析：答案：B
	String类重写了equal()，类型不同返回false
	A. true  s和t指向内存常量区的同一个字符串 
	B. false 一个返回字符串，一个返回对象 ;
	C. true  s和t指向内存常量区的同一个字符串 ;
	D. true equal用于比较两个对象的值是否相同,和内存地址无关
```

##### 2. 有这么一段程序：

```
public class Test{ 
    public String name="abc"; 
    public static void main(String[] args){ 
        Test test=new Test(); 
        Test testB=new Test(); 
        System.out.println(test.equals(testB)+","+test.name.equals(testB.name)); 
    } 
}
```

请问以上程序执行的结果是（）

```

A. true,true
B. true,false
C. false,true
D. false,false
```

```
 解析：答案：C
 	Object 中euqals的源码如上。
 	没有重写equals时，是直接用==判断.
 	String中重写了equals方法。==和！=比较的是对象的引用
```

##### 3. 下列java程序输出结果为()

```
int i=0;
Integer j = new Integer(0);
System.out.println(i==j);
System.out.println(j.equals(i));
```

```
 A. true,false
 B. true,true
 C. false,true
 D. false,false
 E. 对于不同的环境结果不同
 F. 程序无法执行
```

```
解析：答案：B
    1、基本型和基本型封装型进行“==”运算符的比较：
        基本型封装型将会自动拆箱变为基本型后再进行比较，
        因此Integer(0)会自动拆箱为int类型再进行比较，显然返回true；
    2、两个Integer类型进行“==”比较
        如果其值在-128至127，那么返回true，否则返回false, 
        这跟Integer.valueOf()的缓冲对象有关，这里不进行赘述。
    3、两个基本型的封装型进行equals()比较：
        首先equals()会比较类型，如果类型相同，则继续比较值，如果值也相同，返回true
    4、基本型封装类型调用equals(),但是参数是基本类型：
    	这时候，先会进行自动装箱，基本型转换为其封装类型，再进行比较。
```

##### 4. 关于以下程序段，正确的是（）

```
String s1="abc"+"def";//1
String s2=new String（s1);//2
if(s1.equals(s2))//3
	System.out.println(".equals succeeded");//4
if(s1==s2)//5
	System.out.println("==succeeded");//6
```

```
A. 行4，行6都不执行
B. 行6执行，行4不执行
C. 行4执行，行6不执行
D. 行4，行6都将执行
```

```
解析：答案：C
    equal比较类型，在比较值
    ==比较的是地址
```

##### 5. 以下代码执行的结果显示是多少？（）

```
public class Demo {
	public static void main(String[] args) {
		Integer i1 = 128;
        Integer i2 = 128;
        System.out.println((i1==i2)+",");
        String i3 = "100";
        String i4 = "1" + new String("00");
        System.out.println((i3==i4)+",");
        Integer i5 = 100;
        Integer i6 = 100;
        System.out.println((i5==i6));
	}
}
```

```
 A true,false,true
 B false,true,false
 C true,true,false
 D false,false,true
```

```
解析：答案：D
    对于Integer，需要注意的是赋值区间为[-128, 127]时，"=="比较是相等的。
    Integer会对区间为[-128, 127]的数字进行缓存，所以对于 i5和i6来说其实是相等的。
    超出的部分，比如i1和i2是需要重新new一个对象，所以两者不相等。
    对于 i3和i4，明显的是不相等的。
```

#### 每日一句

```
Experience is the name every one gives to their mistakes.
经验是一个人给自己所犯的错误取的名字。
```

发表于 

* 微信号 - xlLoveLove
* https://blog.csdn.net/jdliyao/article/details/79823053