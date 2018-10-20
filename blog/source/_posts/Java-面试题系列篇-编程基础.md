---
title: Java-面试题系列篇-编程基础
date: 2018-10-19 16:18:51
tags: Java
---

本文主要是对近年来出现的Java面试题进行整理汇总，方便大家更好的准备面试.

<!--more-->

## 编程基础

### 面向对象的特征有哪些方面？ 

答：面向对象的特征主要有以下几个方面： 

抽象：抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么。 

继承：继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的重要手段（如果不能理解请阅读阎宏博士的《Java与模式》或《设计模式精解》中关于桥梁模式的部分）。 

封装：通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口（可以想想普通洗衣机和全自动洗衣机的差别，明显全自动洗衣机封装更好因此操作起来更简单；我们现在使用的智能手机也是封装得足够好的，因为几个按键就搞定了所有的事情）。 

多态性：多态性是指允许不同子类型的对象对同一消息作出不同的响应。简单的说就是用同样的对象引用调用同样的方法但是做了不同的事情。多态性分为编译时的多态性和运行时的多态性。如果将对象的方法视为对象向外界提供的服务，那么运行时的多态性可以解释为：当A系统访问B系统提供的服务时，B系统有多种提供服务的方式，但一切对A系统来说都是透明的（就像电动剃须刀是A系统，它的供电系统是B系统，B系统可以使用电池供电或者用交流电，甚至还有可能是太阳能，A系统只会通过B类对象调用供电的方法，但并不知道供电系统的底层实现是什么，究竟通过何种方式获得了动力）。方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1). 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2). 对象造型（用父类型引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。

### 访问修饰符有哪些？区别？

| 修饰符    | 当前类 | 同 包 | 子 类 | 其他包 |
| --------- | ------ | ----- | ----- | ------ |
| public    | √      | √     | √     | √      |
| protected | √      | √     | √     | ×      |
| default   | √      | √     | ×     | ×      |
| private   | √      | ×     | ×     | ×      |

### String 是最基本的数据类型吗？

答：不是。Java中的基本数据类型只有8个：byte、short、int、long、float、double、char、boolean；除了基本类型（primitive type），剩下的都是引用类型（reference type），Java 5以后引入的枚举类型也算是一种比较特殊的引用类型。

### float f=3.4;是否正确？ 

答:不正确。3.4是双精度数，将双精度型（double）赋值给浮点型（float）属于下转型（down-casting，也称为窄化）会造成精度损失，因此需要强制类型转换float f =(float)3.4; 或者写成float f =3.4F。

### short s1 = 1; s1 = s1 + 1;有错吗?short s1 = 1; s1 += 1;有错吗？ 

答：对于short s1 = 1; s1 = s1 + 1;由于1是int类型，因此s1+1运算结果也是int 型，需要强制转换类型才能赋值给short型。而short s1 = 1; s1 += 1;可以正确编译，因为s1+= 1;相当于s1 = (short)(s1 + 1);其中有隐含的强制类型转换。

### Java有没有goto？ 

答：goto 是Java中的保留字，在目前版本的Java中没有使用。（根据James Gosling（Java之父）编写的《The Java Programming Language》一书的附录中给出了一个Java关键字列表，其中有goto和const，但是这两个是目前无法使用的关键字，因此有些地方将其称之为保留字，其实保留字这个词应该有更广泛的意义，因为熟悉C语言的程序员都知道，在系统类库中使用过的有特殊意义的单词或单词的组合都被视为保留字）

### int和Integer有什么区别？ 

答：Java是一个近乎纯洁的面向对象编程语言，但是为了编程的方便还是引入了基本数据类型，但是为了能够将这些基本数据类型当成对象操作，Java为每一个基本数据类型都引入了对应的包装类型（wrapper class），int的包装类就是Integer，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以相互转换。 
Java 为每个原始类型提供了包装类型： 
- 原始类型: boolean，char，byte，short，int，long，float，double 
- 包装类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double

class AutoUnboxingTest {

 

​    public static void main(String[] args) {

​        Integer a = new Integer(3);

​        Integer b = 3;                  // 将3自动装箱成Integer类型

​        int c = 3;

​        System.out.println(a == b);     // false 两个引用没有引用同一对象

​        System.out.println(a == c);     // true a自动拆箱成int类型再和c比较

​    }

}

最近还遇到一个面试题，也是和自动装箱和拆箱有点关系的，代码如下所示：

public class Test03 {

 

​    public static void main(String[] args) {

​        Integer f1 = 100, f2 = 100, f3 = 150, f4 = 150;

 

​        System.out.println(f1 == f2);

​        System.out.println(f3 == f4);

​    }

}

如果不明就里很容易认为两个输出要么都是true要么都是false。首先需要注意的是f1、f2、f3、f4四个变量都是Integer对象引用，所以下面的==运算比较的不是值而是引用。装箱的本质是什么呢？当我们给一个Integer对象赋一个int值的时候，会调用Integer类的静态方法valueOf，如果看看valueOf的源代码就知道发生了什么。

​    public static Integer valueOf(int i) {

​        if (i >= IntegerCache.low && i <= IntegerCache.high)

​            return IntegerCache.cache[i + (-IntegerCache.low)];

​        return new Integer(i);

​    }

IntegerCache是Integer的内部类，其代码如下所示：

/**

​     * Cache to support the object identity semantics of autoboxing for values between

​     * -128 and 127 (inclusive) as required by JLS.

​     *

​     * The cache is initialized on first usage.  The size of the cache

​     * may be controlled by the {@code -XX:AutoBoxCacheMax=<size>} option.

​     * During VM initialization, java.lang.Integer.IntegerCache.high property

​     * may be set and saved in the private system properties in the

​     * sun.misc.VM class.

​     */

 

​    private static class IntegerCache {

​        static final int low = -128;

​        static final int high;

​        static final Integer cache[];

 

​        static {

​            // high value may be configured by property

​            int h = 127;

​            String integerCacheHighPropValue =

​                sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");

​            if (integerCacheHighPropValue != null) {

​                try {

​                    int i = parseInt(integerCacheHighPropValue);

​                    i = Math.max(i, 127);

​                    // Maximum array size is Integer.MAX_VALUE

​                    h = Math.min(i, Integer.MAX_VALUE - (-low) -1);

​                } catch( NumberFormatException nfe) {

​                    // If the property cannot be parsed into an int, ignore it.

​                }

​            }

​            high = h;

 

​            cache = new Integer[(high - low) + 1];

​            int j = low;

​            for(int k = 0; k < cache.length; k++)

​                cache[k] = new Integer(j++);

 

​            // range [-128, 127] must be interned (JLS7 5.1.7)

​            assert IntegerCache.high >= 127;

​        }

 

​        private IntegerCache() {}

​    }

简单的说，如果整型字面量的值在-128到127之间，那么不会new新的Integer对象，而是直接引用常量池中的Integer对象，所以上面的面试题中f1==f2的结果是true，而f3==f4的结果是false。

提醒：越是貌似简单的面试题其中的玄机就越多，需要面试者有相当深厚的功力。

### &和&&的区别？ 

答：&运算符有两种用法：(1)按位与；(2)逻辑与。&&运算符是短路与运算。逻辑与跟短路与的差别是非常巨大的，虽然二者都要求运算符左右两端的布尔值都是true整个表达式的值才是true。&&之所以称为短路运算是因为，如果&&左边的表达式的值是false，右边的表达式会被直接短路掉，不会进行运算。很多时候我们可能都需要用&&而不是&，例如在验证用户登录时判定用户名不是null而且不是空字符串，应当写为：username != null &&!username.equals("")，二者的顺序不能交换，更不能用&运算符，因为第一个条件如果不成立，根本不能进行字符串的equals比较，否则会产生NullPointerException异常。注意：逻辑或运算符（|）和短路或运算符（||）的差别也是如此。

补充：如果你熟悉JavaScript，那你可能更能感受到短路运算的强大，想成为JavaScript的高手就先从玩转短路运算开始吧。

### 解释内存中的栈(stack)、堆(heap)和方法区(method area)的用法。 

答：通常我们定义一个基本数据类型的变量，一个对象的引用，还有就是函数调用的现场保存都使用JVM中的栈空间；而通过new关键字和构造器创建的对象则放在堆空间，堆是垃圾收集器管理的主要区域，由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，再具体一点可以分为Eden、Survivor（又可分为From Survivor和To Survivor）、Tenured；方法区和堆都是各个线程共享的内存区域，用于存储已经被JVM加载的类信息、常量、静态变量、JIT编译器编译后的代码等数据；程序中的字面量（literal）如直接书写的100、"hello"和常量都是放在常量池中，常量池是方法区的一部分，。栈空间操作起来最快但是栈很小，通常大量的对象都是放在堆空间，栈和堆的大小都可以通过JVM的启动参数来进行调整，栈空间用光了会引发StackOverflowError，而堆和常量池空间不足则会引发OutOfMemoryError。

String str = new String("hello");

上面的语句中变量str放在栈上，用new创建出来的字符串对象放在堆上，而"hello"这个字面量是放在方法区的。

补充1：较新版本的Java（从Java 6的某个更新开始）中，由于JIT编译器的发展和"逃逸分析"技术的逐渐成熟，栈上分配、标量替换等优化技术使得对象一定分配在堆上这件事情已经变得不那么绝对了。

补充2：运行时常量池相当于Class文件常量池具有动态性，Java语言并不要求常量一定只有编译期间才能产生，运行期间也可以将新的常量放入池中，String类的intern()方法就是这样的。

看看下面代码的执行结果是什么并且比较一下Java 7以前和以后的运行结果是否一致。

String s1 = new StringBuilder("go")

​    .append("od").toString();

System.out.println(s1.intern() == s1);

String s2 = new StringBuilder("ja")

​    .append("va").toString();

System.out.println(s2.intern() == s2);

### Math.round(11.5) 等于多少？Math.round(-11.5)等于多少？

 答：Math.round(11.5)的返回值是12，Math.round(-11.5)的返回值是-11。四舍五入的原理是在参数上加0.5然后向下取整。

### switch 是否能作用在byte 上，是否能作用在long 上，是否能作用在String上？ 

答：

（1）在Java 5以前，switch(expr)中，expr只能是byte、short、char、int。

（2）从Java 5开始，Java中引入了枚举类型，expr也可以是enum类型，

（3）从Java 7开始，expr还可以是字符串（String）。

但是长整型（long）在目前所有的版本中都是不可以的。

### 用最有效率的方法计算2乘以8？ 

答： 2 << 3（左移3位相当于乘以2的3次方，右移3位相当于除以2的3次方）。

补充：我们为编写的类重写hashCode方法时，可能会看到如下所示的代码，其实我们不太理解为什么要使用这样的乘法运算来产生哈希码（散列码），而且为什么这个数是个素数，为什么通常选择31这个数？前两个问题的答案你可以自己百度一下，选择31是因为可以用移位和减法运算来代替乘法，从而得到更好的性能。说到这里你可能已经想到了：31 * num 等价于(num << 5) - num，左移5位相当于乘以2的5次方再减去自身就相当于乘以31，现在的VM都能自动完成这个优化。

public class PhoneNumber {

​    private int areaCode;

​    private String prefix;

​    private String lineNumber;

 

​    @Override

​    public int hashCode() {

​        final int prime = 31;

​        int result = 1;

​        result = prime * result + areaCode;

​        result = prime * result

​                + ((lineNumber == null) ? 0 : lineNumber.hashCode());

​        result = prime * result + ((prefix == null) ? 0 : prefix.hashCode());

​        return result;

​    }

 

​    @Override

​    public boolean equals(Object obj) {

​        if (this == obj)

​            return true;

​        if (obj == null)

​            return false;

​        if (getClass() != obj.getClass())

​            return false;

​        PhoneNumber other = (PhoneNumber) obj;

​        if (areaCode != other.areaCode)

​            return false;

​        if (lineNumber == null) {

​            if (other.lineNumber != null)

​                return false;

​        } else if (!lineNumber.equals(other.lineNumber))

​            return false;

​        if (prefix == null) {

​            if (other.prefix != null)

​                return false;

​        } else if (!prefix.equals(other.prefix))

​            return false;

​        return true;

​    }

 

}

### 数组有没有length()方法？String有没有length()方法？ 

答：数组没有length()方法，有length 的属性。String 有length()方法。JavaScript中，获得字符串的长度是通过length属性得到的，这一点容易和Java混淆。

### 在Java中，如何跳出当前的多重嵌套循环？ 

答：在最外层循环前加一个标记如A，然后用break A;可以跳出多重循环。（Java中支持带标签的break和continue语句，作用有点类似于C和C++中的goto语句，但是就像要避免使用goto一样，应该避免使用带标签的break和continue，因为它不会让你的程序变得更优雅，很多时候甚至有相反的作用，所以这种语法其实不知道更好）

### 构造器（constructor）是否可被重写（override）？ 

答：构造器不能被继承，因此不能被重写，但可以被重载。

### 两个对象值相同(x.equals(y) == true)，但却可有不同的hash code，这句话对不对？ 

答：不对，如果两个对象x和y满足x.equals(y) == true，它们的哈希码（hash code）应当相同。Java对于eqauls方法和hashCode方法是这样规定的：(1)如果两个对象相同（equals方法返回true），那么它们的hashCode值一定要相同；(2)如果两个对象的hashCode相同，它们并不一定相同。当然，你未必要按照要求去做，但是如果你违背了上述原则就会发现在使用容器时，相同的对象可以出现在Set集合中，同时增加新元素的效率会大大下降（对于使用哈希存储的系统，如果哈希码频繁的冲突将会造成存取性能急剧下降）。

补充：关于equals和hashCode方法，很多Java程序都知道，但很多人也就是仅仅知道而已，在Joshua Bloch的大作《Effective Java》（很多软件公司，《Effective Java》、《Java编程思想》以及《重构：改善既有代码质量》是Java程序员必看书籍，如果你还没看过，那就赶紧去亚马逊买一本吧）中是这样介绍equals方法的：首先equals方法必须满足自反性（x.equals(x)必须返回true）、对称性（x.equals(y)返回true时，y.equals(x)也必须返回true）、传递性（x.equals(y)和y.equals(z)都返回true时，x.equals(z)也必须返回true）和一致性（当x和y引用的对象信息没有被修改时，多次调用x.equals(y)应该得到同样的返回值），而且对于任何非null值的引用x，x.equals(null)必须返回false。实现高质量的equals方法的诀窍包括：1. 使用==操作符检查"参数是否为这个对象的引用"；2. 使用instanceof操作符检查"参数是否为正确的类型"；3. 对于类中的关键属性，检查参数传入对象的属性是否与之相匹配；4. 编写完equals方法后，问自己它是否满足对称性、传递性、一致性；5. 重写equals时总是要重写hashCode；6. 不要将equals方法参数中的Object对象替换为其他的类型，在重写时不要忘掉@Override注解。

### 是否可以继承String类？ 

答：String 类是final类，不可以被继承。

补充：继承String本身就是一个错误的行为，对String类型最好的重用方式是关联关系（Has-A）和依赖关系（Use-A）而不是继承关系（Is-A）。

### 当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递？ 

答：是值传递。Java语言的方法调用只支持参数的值传递。当一个对象实例作为一个参数被传递到方法中时，参数的值就是对该对象的引用。对象的属性可以在被调用过程中被改变，但对对象引用的改变是不会影响到调用者的。C++和C#中可以通过传引用或传输出参数来改变传入的参数的值。在C#中可以编写如下所示的代码，但是在Java中却做不到。

using System;

 

namespace CS01 {

 

​    class Program {

​        public static void swap(ref int x, ref int y) {

​            int temp = x;

​            x = y;

​            y = temp;

​        }

 

​        public static void Main (string[] args) {

​            int a = 5, b = 10;

​            swap (ref a, ref b);

​            // a = 10, b = 5;

​            Console.WriteLine ("a = {0}, b = {1}", a, b);

​        }

​    }

}

说明：Java中没有传引用实在是非常的不方便，这一点在Java 8中仍然没有得到改进，正是如此在Java编写的代码中才会出现大量的Wrapper类（将需要通过方法调用修改的引用置于一个Wrapper类中，再将Wrapper对象传入方法），这样的做法只会让代码变得臃肿，尤其是让从C和C++转型为Java程序员的开发者无法容忍。

### String和StringBuilder、StringBuffer的区别？

 答：Java平台提供了两种类型的字符串：String和StringBuffer/StringBuilder，它们可以储存和操作字符串。其中String是只读字符串，也就意味着String引用的字符串内容是不能被改变的。而StringBuffer/StringBuilder类表示的字符串对象可以直接进行修改。StringBuilder是Java 5中引入的，它和StringBuffer的方法完全相同，区别在于它是在单线程环境下使用的，因为它的所有方面都没有被synchronized修饰，因此它的效率也比StringBuffer要高。

面试题1 - 什么情况下用+运算符进行字符串连接比调用StringBuffer/StringBuilder对象的append方法连接字符串性能更好？

面试题2 - 请说出下面程序的输出。

class StringEqualTest {

 

​    public static void main(String[] args) {

​        String s1 = "Programming";

​        String s2 = new String("Programming");

​        String s3 = "Program";

​        String s4 = "ming";

​        String s5 = "Program" + "ming";

​        String s6 = s3 + s4;

​        System.out.println(s1 == s2);

​        System.out.println(s1 == s5);

​        System.out.println(s1 == s6);

​        System.out.println(s1 == s6.intern());

​        System.out.println(s2 == s2.intern());

​    }

}

补充：解答上面的面试题需要清楚两点：1. String对象的intern方法会得到字符串对象在常量池中对应的版本的引用（如果常量池中有一个字符串与String对象的equals结果是true），如果常量池中没有对应的字符串，则该字符串将被添加到常量池中，然后返回常量池中字符串的引用；2. 字符串的+操作其本质是创建了StringBuilder对象进行append操作，然后将拼接后的StringBuilder对象用toString方法处理成String对象，这一点可以用javap -c StringEqualTest.class命令获得class文件对应的JVM字节码指令就可以看出来。

### 重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？ 

答：方法的重载和重写都是实现多态的方式，区别在于前者实现的是编译时的多态性，而后者实现的是运行时的多态性。重载发生在一个类中，同名的方法如果有不同的参数列表（参数类型不同、参数个数不同或者二者都不同）则视为重载；重写发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的返回类型，比父类被重写方法更好访问，不能比父类被重写方法声明更多的异常（里氏代换原则）。重载对返回类型没有特殊的要求。

面试题：华为的面试题中曾经问过这样一个问题 - "为什么不能根据返回类型来区分重载"，快说出你的答案吧！

### 描述一下JVM加载class文件的原理机制？ 

答：JVM中类的装载是由类加载器（ClassLoader）和它的子类来实现的，Java中的类加载器是一个重要的Java运行时系统组件，它负责在运行时查找和装入类文件中的类。 
由于Java的跨平台性，经过编译的Java源程序并不是一个可执行程序，而是一个或多个类文件。当Java程序需要使用某个类时，JVM会确保这个类已经被加载、连接（验证、准备和解析）和初始化。类的加载是指把类的.class文件中的数据读入到内存中，通常是创建一个字节数组读入.class文件，然后产生与所加载类对应的Class对象。加载完成后，Class对象还不完整，所以此时的类还不可用。当类被加载后就进入连接阶段，这一阶段包括验证、准备（为静态变量分配内存并设置默认的初始值）和解析（将符号引用替换为直接引用）三个步骤。最后JVM对类进行初始化，包括：1)如果类存在直接的父类并且这个类还没有被初始化，那么就先初始化父类；2)如果类中存在初始化语句，就依次执行这些初始化语句。 
类的加载是由类加载器完成的，类加载器包括：根加载器（BootStrap）、扩展加载器（Extension）、系统加载器（System）和用户自定义类加载器（java.lang.ClassLoader的子类）。从Java 2（JDK 1.2）开始，类加载过程采取了父亲委托机制（PDM）。PDM更好的保证了Java平台的安全性，在该机制中，JVM自带的Bootstrap是根加载器，其他的加载器都有且仅有一个父类加载器。类的加载首先请求父类加载器加载，父类加载器无能为力时才由其子类加载器自行加载。JVM不会向Java程序提供对Bootstrap的引用。下面是关于几个类加载器的说明：

Bootstrap：一般用本地代码实现，负责加载JVM基础核心类库（rt.jar）；

Extension：从java.ext.dirs系统属性所指定的目录中加载类库，它的父加载器是Bootstrap；

System：又叫应用类加载器，其父类是Extension。它是应用最广泛的类加载器。它从环境变量classpath或者系统属性java.class.path所指定的目录中记载类，是用户自定义加载器的默认父加载器。

### char 型变量中能不能存贮一个中文汉字，为什么？

 答：char类型可以存储一个中文汉字，因为Java中使用的编码是Unicode（不选择任何特定的编码，直接使用字符在字符集中的编号，这是统一的唯一方法），一个char类型占2个字节（16比特），所以放一个中文是没问题的。

补充：使用Unicode意味着字符在JVM内部和外部有不同的表现形式，在JVM内部都是Unicode，当这个字符被从JVM内部转移到外部时（例如存入文件系统中），需要进行编码转换。所以Java中有字节流和字符流，以及在字符流和字节流之间进行转换的转换流，如InputStreamReader和OutputStreamReader，这两个类是字节流和字符流之间的适配器类，承担了编码转换的任务；对于C程序员来说，要完成这样的编码转换恐怕要依赖于union（联合体/共用体）共享内存的特征来实现了。

### 抽象类（abstract class）和接口（interface）有什么异同？ 

答：抽象类和接口都不能够实例化，但可以定义抽象类和接口类型的引用。一个类如果继承了某个抽象类或者实现了某个接口都需要对其中的抽象方法全部进行实现，否则该类仍然需要被声明为抽象类。接口比抽象类更加抽象，因为抽象类中可以定义构造器，可以有抽象方法和具体方法，而接口中不能定义构造器而且其中的方法全部都是抽象方法。抽象类中的成员可以是private、默认、protected、public的，而接口中的成员全都是public的。抽象类中可以定义成员变量，而接口中定义的成员变量实际上都是常量。有抽象方法的类必须被声明为抽象类，而抽象类未必要有抽象方法。

### 静态嵌套类(Static Nested Class)和内部类（Inner Class）的不同？

 答：Static Nested Class是被声明为静态（static）的内部类，它可以不依赖于外部类实例被实例化。而通常的内部类需要在外部类实例化后才能实例化，其语法看起来挺诡异的，如下所示。

/**

 * 扑克类（一副扑克）

 * @author 骆昊

 *

 */

public class Poker {

​    private static String[] suites = {"黑桃", "红桃", "草花", "方块"};

​    private static int[] faces = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13};

 

​    private Card[] cards;

 

​    /**

​     * 构造器

​     * 

​     */

​    public Poker() {

​        cards = new Card[52];

​        for(int i = 0; i < suites.length; i++) {

​            for(int j = 0; j < faces.length; j++) {

​                cards[i * 13 + j] = new Card(suites[i], faces[j]);

​            }

​        }

​    }

 

​    /**

​     * 洗牌 （随机乱序）

​     * 

​     */

​    public void shuffle() {

​        for(int i = 0, len = cards.length; i < len; i++) {

​            int index = (int) (Math.random() * len);

​            Card temp = cards[index];

​            cards[index] = cards[i];

​            cards[i] = temp;

​        }

​    }

 

​    /**

​     * 发牌

​     * @param index 发牌的位置

​     * 

​     */

​    public Card deal(int index) {

​        return cards[index];

​    }

 

​    /**

​     * 卡片类（一张扑克）

​     * [内部类]

​     * @author 骆昊

​     *

​     */

​    public class Card {

​        private String suite;   // 花色

​        private int face;       // 点数

 

​        public Card(String suite, int face) {

​            this.suite = suite;

​            this.face = face;

​        }

 

​        @Override

​        public String toString() {

​            String faceStr = "";

​            switch(face) {

​            case 1: faceStr = "A"; break;

​            case 11: faceStr = "J"; break;

​            case 12: faceStr = "Q"; break;

​            case 13: faceStr = "K"; break;

​            default: faceStr = String.valueOf(face);

​            }

​            return suite + faceStr;

​        }

​    }

}

测试代码：

class PokerTest {

 

​    public static void main(String[] args) {

​        Poker poker = new Poker();

​        poker.shuffle();                // 洗牌

​        Poker.Card c1 = poker.deal(0);  // 发第一张牌

​        // 对于非静态内部类Card

​        // 只有通过其外部类Poker对象才能创建Card对象

​        Poker.Card c2 = poker.new Card("红心", 1);    // 自己创建一张牌

 

​        System.out.println(c1);     // 洗牌后的第一张

​        System.out.println(c2);     // 打印: 红心A

​    }

}

面试题 - 下面的代码哪些地方会产生编译错误？

class Outer {

 

​    class Inner {}

 

​    public static void foo() { new Inner(); }

 

​    public void bar() { new Inner(); }

 

​    public static void main(String[] args) {

​        new Inner();

​    }

}

注意：Java中非静态内部类对象的创建要依赖其外部类对象，上面的面试题中foo和main方法都是静态方法，静态方法中没有this，也就是说没有所谓的外部类对象，因此无法创建内部类对象，如果要在静态方法中创建内部类对象，可以这样做：

new Outer().new Inner();

### 抽象的（abstract）方法是否可同时是静态的（static）,是否可同时是本地方法（native），是否可同时被synchronized修饰？

 答：都不能。抽象方法需要子类重写，而静态的方法是无法被重写的，因此二者是矛盾的。本地方法是由本地代码（如C代码）实现的方法，而抽象方法是没有实现的，也是矛盾的。synchronized和方法的实现细节有关，抽象方法不涉及实现细节，因此也是相互矛盾的。

### 阐述静态变量和实例变量的区别。

 答：静态变量是被static修饰符修饰的变量，也称为类变量，它属于类，不属于类的任何一个对象，一个类不管创建多少个对象，静态变量在内存中有且仅有一个拷贝；实例变量必须依存于某一实例，需要先创建对象然后通过对象才能访问到它。静态变量可以实现让多个对象共享内存。

补充：在Java开发中，上下文类和工具类中通常会有大量的静态成员。

### 是否可以从一个静态（static）方法内部发出对非静态（non-static）方法的调用？ 

答：不可以，静态方法只能访问静态成员，因为非静态方法的调用要先创建对象，在调用静态方法时可能对象并没有被初始化。

### 如何实现对象克隆？

 答：有两种方式： 
  1). 实现Cloneable接口并重写Object类中的clone()方法； 
  2). 实现Serializable接口，通过对象的序列化和反序列化实现克隆，可以实现真正的深度克隆，代码如下。

import java.io.ByteArrayInputStream;

import java.io.ByteArrayOutputStream;

import java.io.ObjectInputStream;

import java.io.ObjectOutputStream;

import java.io.Serializable;

 

public class MyUtil {

 

​    private MyUtil() {

​        throw new AssertionError();

​    }

 

​    @SuppressWarnings("unchecked")

​    public static <T extends Serializable> T clone(T obj) throws Exception {

​        ByteArrayOutputStream bout = new ByteArrayOutputStream();

​        ObjectOutputStream oos = new ObjectOutputStream(bout);

​        oos.writeObject(obj);

 

​        ByteArrayInputStream bin = new ByteArrayInputStream(bout.toByteArray());

​        ObjectInputStream ois = new ObjectInputStream(bin);

​        return (T) ois.readObject();

 

​        // 说明：调用ByteArrayInputStream或ByteArrayOutputStream对象的close方法没有任何意义

​        // 这两个基于内存的流只要垃圾回收器清理对象就能够释放资源，这一点不同于对外部资源（如文件流）的释放

​    }

}

下面是测试代码：

import java.io.Serializable;

 

/**

 * 人类

 * @author 骆昊

 *

 */

class Person implements Serializable {

​    private static final long serialVersionUID = -9102017020286042305L;

 

​    private String name;    // 姓名

​    private int age;        // 年龄

​    private Car car;        // 座驾

 

​    public Person(String name, int age, Car car) {

​        this.name = name;

​        this.age = age;

​        this.car = car;

​    }

 

​    public String getName() {

​        return name;

​    }

 

​    public void setName(String name) {

​        this.name = name;

​    }

 

​    public int getAge() {

​        return age;

​    }

 

​    public void setAge(int age) {

​        this.age = age;

​    }

 

​    public Car getCar() {

​        return car;

​    }

 

​    public void setCar(Car car) {

​        this.car = car;

​    }

 

​    @Override

​    public String toString() {

​        return "Person [name=" + name + ", age=" + age + ", car=" + car + "]";

​    }

 

}

/**

 * 小汽车类

 * @author 骆昊

 *

 */

class Car implements Serializable {

​    private static final long serialVersionUID = -5713945027627603702L;

 

​    private String brand;       // 品牌

​    private int maxSpeed;       // 最高时速

 

​    public Car(String brand, int maxSpeed) {

​        this.brand = brand;

​        this.maxSpeed = maxSpeed;

​    }

 

​    public String getBrand() {

​        return brand;

​    }

 

​    public void setBrand(String brand) {

​        this.brand = brand;

​    }

 

​    public int getMaxSpeed() {

​        return maxSpeed;

​    }

 

​    public void setMaxSpeed(int maxSpeed) {

​        this.maxSpeed = maxSpeed;

​    }

 

​    @Override

​    public String toString() {

​        return "Car [brand=" + brand + ", maxSpeed=" + maxSpeed + "]";

​    }

 

}

class CloneTest {

 

​    public static void main(String[] args) {

​        try {

​            Person p1 = new Person("Hao LUO", 33, new Car("Benz", 300));

​            Person p2 = MyUtil.clone(p1);   // 深度克隆

​            p2.getCar().setBrand("BYD");

​            // 修改克隆的Person对象p2关联的汽车对象的品牌属性

​            // 原来的Person对象p1关联的汽车不会受到任何影响

​            // 因为在克隆Person对象时其关联的汽车对象也被克隆了

​            System.out.println(p1);

​        } catch (Exception e) {

​            e.printStackTrace();

​        }

​    }

}

注意：基于序列化和反序列化实现的克隆不仅仅是深度克隆，更重要的是通过泛型限定，可以检查出要克隆的对象是否支持序列化，这项检查是编译器完成的，不是在运行时抛出异常，这种是方案明显优于使用Object类的clone方法克隆对象。让问题在编译的时候暴露出来总是好过把问题留到运行时。

### String s = new String("xyz");创建了几个字符串对象？ 

答：两个对象，一个是静态区的"xyz"，一个是用new创建在堆上的对象。

### 接口是否可继承（extends）接口？抽象类是否可实现（implements）接口？抽象类是否可继承具体类（concrete class）？

 答：接口可以继承接口，而且支持多重继承。抽象类可以实现(implements)接口，抽象类可继承具体类也可以继承抽象类。

### 一个".java"源文件中是否可以包含多个类（不是内部类）？有什么限制？

 答：可以，但一个源文件中最多只能有一个公开类（public class）而且文件名必须和公开类的类名完全保持一致。

### Anonymous Inner Class(匿名内部类)是否可以继承其它类？是否可以实现接口？

 答：可以继承其他类或实现其他接口，在Swing编程和Android开发中常用此方式来实现事件监听和回调。

### 内部类可以引用它的包含类（外部类）的成员吗？有没有什么限制？

 答：一个内部类对象可以访问创建它的外部类对象的成员，包括私有成员。

### Java 中的final关键字有哪些用法？

 答：

(1)修饰类：表示该类不能被继承；

(2)修饰方法：表示方法不能被重写；

(3)修饰变量：表示变量只能一次赋值以后值不能被修改（常量）。

### 指出下面程序的运行结果。

class A {

 

​    static {

​        System.out.print("1");

​    }

 

​    public A() {

​        System.out.print("2");

​    }

}

 

class B extends A{

 

​    static {

​        System.out.print("a");

​    }

 

​    public B() {

​        System.out.print("b");

​    }

}

 

public class Hello {

 

​    public static void main(String[] args) {

​        A ab = new B();

​        ab = new B();

​    }

 

}

答：执行结果：1a2b2b。

创建对象时构造器的调用顺序是：

先初始化静态成员，

然后调用父类构造器，

再初始化非静态成员，

最后调用自身构造器。

提示：如果不能给出此题的正确答案，说明之前第21题Java类加载机制还没有完全理解，赶紧再看看吧。

### 数据类型之间的转换：  - 如何将字符串转换为基本数据类型？  - 如何将基本数据类型转换为字符串？ 

答： 
- 调用基本数据类型对应的包装类中的方法parseXXX(String)或valueOf(String)即可返回相应基本类型； 
- 一种方法是将基本数据类型与空字符串（""）连接（+）即可获得其所对应的字符串；另一种方法是调用String 类中的valueOf()方法返回相应字符串

### 如何实现字符串的反转及替换？ 

答：方法很多，可以自己写实现也可以使用String或StringBuffer/StringBuilder中的方法。有一道很常见的面试题是用递归实现字符串反转，代码如下所示：

​    public static String reverse(String originStr) {

​        if(originStr == null || originStr.length() <= 1) 

​            return originStr;

​        return reverse(originStr.substring(1)) + originStr.charAt(0);

​    }

### 怎样将GB2312编码的字符串转换为ISO-8859-1编码的字符串？ 

答：代码如下所示：

String s1 = "你好";

String s2 = new String(s1.getBytes("GB2312"), "ISO-8859-1");

### 日期和时间：  - 如何取得年月日、小时分钟秒？  - 如何取得从1970年1月1日0时0分0秒到现在的毫秒数？  - 如何取得某月的最后一天？  - 如何格式化日期？

 答： 
问题1：创建java.util.Calendar 实例，调用其get()方法传入不同的参数即可获得参数所对应的值。Java 8中可以使用java.time.LocalDateTimel来获取，代码如下所示。

public class DateTimeTest {

​    public static void main(String[] args) {

​        Calendar cal = Calendar.getInstance();

​        System.out.println(cal.get(Calendar.YEAR));

​        System.out.println(cal.get(Calendar.MONTH));    // 0 - 11

​        System.out.println(cal.get(Calendar.DATE));

​        System.out.println(cal.get(Calendar.HOUR_OF_DAY));

​        System.out.println(cal.get(Calendar.MINUTE));

​        System.out.println(cal.get(Calendar.SECOND));

 

​        // Java 8

​        LocalDateTime dt = LocalDateTime.now();

​        System.out.println(dt.getYear());

​        System.out.println(dt.getMonthValue());     // 1 - 12

​        System.out.println(dt.getDayOfMonth());

​        System.out.println(dt.getHour());

​        System.out.println(dt.getMinute());

​        System.out.println(dt.getSecond());

​    }

}

问题2：以下方法均可获得该毫秒数。

Calendar.getInstance().getTimeInMillis();

System.currentTimeMillis();

Clock.systemDefaultZone().millis(); // Java 8

问题3：代码如下所示。

Calendar time = Calendar.getInstance();

time.getActualMaximum(Calendar.DAY_OF_MONTH);

问题4：利用java.text.DataFormat 的子类（如SimpleDateFormat类）中的format(Date)方法可将日期格式化。Java 8中可以用java.time.format.DateTimeFormatter来格式化时间日期，代码如下所示。

import java.text.SimpleDateFormat;

import java.time.LocalDate;

import java.time.format.DateTimeFormatter;

import java.util.Date;

 

class DateFormatTest {

 

​    public static void main(String[] args) {

​        SimpleDateFormat oldFormatter = new SimpleDateFormat("yyyy/MM/dd");

​        Date date1 = new Date();

​        System.out.println(oldFormatter.format(date1));

 

​        // Java 8

​        DateTimeFormatter newFormatter = DateTimeFormatter.ofPattern("yyyy/MM/dd");

​        LocalDate date2 = LocalDate.now();

​        System.out.println(date2.format(newFormatter));

​    }

}

补充：Java的时间日期API一直以来都是被诟病的东西，为了解决这一问题，Java 8中引入了新的时间日期API，其中包括LocalDate、LocalTime、LocalDateTime、Clock、Instant等类，这些的类的设计都使用了不变模式，因此是线程安全的设计。如果不理解这些内容，可以参考我的另一篇文章《关于Java并发编程的总结和思考》。

### 打印昨天的当前时刻。 

答：

import java.util.Calendar;

 

class YesterdayCurrent {

​    public static void main(String[] args){

​        Calendar cal = Calendar.getInstance();

​        cal.add(Calendar.DATE, -1);

​        System.out.println(cal.getTime());

​    }

}

在Java 8中，可以用下面的代码实现相同的功能。

import java.time.LocalDateTime;

 

class YesterdayCurrent {

 

​    public static void main(String[] args) {

​        LocalDateTime today = LocalDateTime.now();

​        LocalDateTime yesterday = today.minusDays(1);

 

​        System.out.println(yesterday);

​    }

}

### 比较一下Java和JavaSciprt。 

答：JavaScript 与Java是两个公司开发的不同的两个产品。Java 是原Sun Microsystems公司推出的面向对象的程序设计语言，特别适合于互联网应用程序开发；而JavaScript是Netscape公司的产品，为了扩展Netscape浏览器的功能而开发的一种可以嵌入Web页面中运行的基于对象和事件驱动的解释性语言。JavaScript的前身是LiveScript；而Java的前身是Oak语言。 
下面对两种语言间的异同作如下比较： 
- 基于对象和面向对象：Java是一种真正的面向对象的语言，即使是开发简单的程序，必须设计对象；JavaScript是种脚本语言，它可以用来制作与网络无关的，与用户交互作用的复杂软件。它是一种基于对象（Object-Based）和事件驱动（Event-Driven）的编程语言，因而它本身提供了非常丰富的内部对象供设计人员使用。 
- 解释和编译：Java的源代码在执行之前，必须经过编译。JavaScript是一种解释性编程语言，其源代码不需经过编译，由浏览器解释执行。（目前的浏览器几乎都使用了JIT（即时编译）技术来提升JavaScript的运行效率） 
- 强类型变量和类型弱变量：Java采用强类型变量检查，即所有变量在编译之前必须作声明；JavaScript中变量是弱类型的，甚至在使用变量前可以不作声明，JavaScript的解释器在运行时检查推断其数据类型。 
- 代码格式不一样。

补充：上面列出的四点是网上流传的所谓的标准答案。其实Java和JavaScript最重要的区别是一个是静态语言，一个是动态语言。目前的编程语言的发展趋势是函数式语言和动态语言。在Java中类（class）是一等公民，而JavaScript中函数（function）是一等公民，因此JavaScript支持函数式编程，可以使用Lambda函数和闭包（closure），当然Java 8也开始支持函数式编程，提供了对Lambda表达式以及函数式接口的支持。对于这类问题，在面试的时候最好还是用自己的语言回答会更加靠谱，不要背网上所谓的标准答案。

### 什么时候用断言（assert）？

 答：断言在软件开发中是一种常用的调试方式，很多开发语言中都支持这种机制。一般来说，断言用于保证程序最基本、关键的正确性。断言检查通常在开发和测试时开启。为了保证程序的执行效率，在软件发布后断言检查通常是关闭的。断言是一个包含布尔表达式的语句，在执行这个语句时假定该表达式为true；如果表达式的值为false，那么系统会报告一个AssertionError。断言的使用如下面的代码所示：

assert(a > 0); // throws an AssertionError if a <= 0

1

断言可以有两种形式： 
assert Expression1; 
assert Expression1 : Expression2 ; 
Expression1 应该总是产生一个布尔值。 
Expression2 可以是得出一个值的任意表达式；这个值用于生成显示更多调试信息的字符串消息。

要在运行时启用断言，可以在启动JVM时使用-enableassertions或者-ea标记。要在运行时选择禁用断言，可以在启动JVM时使用-da或者-disableassertions标记。要在系统类中启用或禁用断言，可使用-esa或-dsa标记。还可以在包的基础上启用或者禁用断言。

注意：断言不应该以任何方式改变程序的状态。简单的说，如果希望在不满足某些条件时阻止代码的执行，就可以考虑用断言来阻止它。

### Error和Exception有什么区别？

 答：Error表示系统级的错误和程序不必处理的异常，是恢复不是不可能但很困难的情况下的一种严重问题；比如内存溢出，不可能指望程序能处理这样的情况；Exception表示需要捕捉或者需要程序进行处理的异常，是一种设计或实现问题；也就是说，它表示如果程序运行正常，从不会发生的情况。

面试题：2005年摩托罗拉的面试中曾经问过这么一个问题“If a process reports a stack overflow run-time error, what’s the most possible cause?”，给了四个选项a. lack of memory; b. write on an invalid memory space; c. recursive function calling; d. array index out of boundary. Java程序在运行时也可能会遭遇StackOverflowError，这是一个无法恢复的错误，只能重新修改代码了，这个面试题的答案是c。如果写了不能迅速收敛的递归，则很有可能引发栈溢出的错误，如下所示：

class StackOverflowErrorTest {

 

​    public static void main(String[] args) {

​        main(null);

​    }

}

提示：用递归编写程序时一定要牢记两点：1. 递归公式；2. 收敛条件（什么时候就不再继续递归）。

### try{}里有一个return语句，那么紧跟在这个try后的finally{}里的代码会不会被执行，什么时候被执行，在return前还是后? 

答：会执行，在方法返回调用者前执行。

注意：在finally中改变返回值的做法是不好的，因为如果存在finally代码块，try中的return语句不会立马返回调用者，而是记录下返回值待finally代码块执行完毕之后再向调用者返回其值，然后如果在finally中修改了返回值，就会返回修改后的值。显然，在finally中返回或者修改返回值会对程序造成很大的困扰，C#中直接用编译错误的方式来阻止程序员干这种龌龊的事情，Java中也可以通过提升编译器的语法检查级别来产生警告或错误，Eclipse中可以在如图所示的地方进行设置，强烈建议将此项设置为编译错误。

### Java语言如何进行异常处理，关键字：throws、throw、try、catch、finally分别如何使用？

 答：Java通过面向对象的方法进行异常处理，把各种不同的异常进行分类，并提供了良好的接口。在Java中，每个异常都是一个对象，它是Throwable类或其子类的实例。当一个方法出现异常后便抛出一个异常对象，该对象中包含有异常信息，调用这个对象的方法可以捕获到这个异常并可以对其进行处理。Java的异常处理是通过5个关键词来实现的：try、catch、throw、throws和finally。一般情况下是用try来执行一段程序，如果系统会抛出（throw）一个异常对象，可以通过它的类型来捕获（catch）它，或通过总是执行代码块（finally）来处理；try用来指定一块预防所有异常的程序；catch子句紧跟在try块后面，用来指定你想要捕获的异常的类型；throw语句用来明确地抛出一个异常；throws用来声明一个方法可能抛出的各种异常（当然声明异常时允许无病呻吟）；finally为确保一段代码不管发生什么异常状况都要被执行；try语句可以嵌套，每当遇到一个try语句，异常的结构就会被放入异常栈中，直到所有的try语句都完成。如果下一级的try语句没有对某种异常进行处理，异常栈就会执行出栈操作，直到遇到有处理这种异常的try语句或者最终将异常抛给JVM。

### 运行时异常与受检异常有何异同？

 答：异常表示程序运行过程中可能出现的非正常状态，运行时异常表示虚拟机的通常操作中可能遇到的异常，是一种常见运行错误，只要程序设计得没有问题通常就不会发生。受检异常跟程序运行的上下文环境有关，即使程序设计无误，仍然可能因使用的问题而引发。Java编译器要求方法必须声明抛出可能发生的受检异常，但是并不要求必须声明抛出未被捕获的运行时异常。异常和继承一样，是面向对象程序设计中经常被滥用的东西，在Effective Java中对异常的使用给出了以下指导原则： 
- 不要将异常处理用于正常的控制流（设计良好的API不应该强迫它的调用者为了正常的控制流而使用异常） 
- 对可以恢复的情况使用受检异常，对编程错误使用运行时异常 
- 避免不必要的使用受检异常（可以通过一些状态检测手段来避免异常的发生） 
- 优先使用标准的异常 
- 每个方法抛出的异常都要有文档 
- 保持异常的原子性 
- 不要在catch中忽略掉捕获到的异常

### 列出一些你常见的运行时异常？ 

答： 
- ArithmeticException（算术异常） 
- ClassCastException （类转换异常） 
- IllegalArgumentException （非法参数异常） 
- IndexOutOfBoundsException （下标越界异常） 
- NullPointerException （空指针异常） 
- SecurityException （安全异常）

### 阐述final、finally、finalize的区别。

 答： 
- final：修饰符（关键字）有三种用法：如果一个类被声明为final，意味着它不能再派生出新的子类，即不能被继承，因此它和abstract是反义词。将变量声明为final，可以保证它们在使用中不被改变，被声明为final的变量必须在声明时给定初值，而在以后的引用中只能读取不可修改。被声明为final的方法也同样只能使用，不能在子类中被重写。 
- finally：通常放在try…catch…的后面构造总是执行代码块，这就意味着程序无论正常执行还是发生异常，这里的代码只要JVM不关闭都能执行，可以将释放外部资源的代码写在finally块中。 
- finalize：Object类中定义的方法，Java中允许使用finalize()方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在销毁对象时调用的，通过重写finalize()方法可以整理系统资源或者执行其他清理工作。

### 类ExampleA继承Exception，类ExampleB继承ExampleA。  有如下代码片断：

try {

​    throw new ExampleB("b")

} catch（ExampleA e）{

​    System.out.println("ExampleA");

} catch（Exception e）{

​    System.out.println("Exception");

}

请问执行此段代码的输出是什么？


答：输出：ExampleA。（根据里氏代换原则[能使用父类型的地方一定能使用子类型]，抓取ExampleA类型异常的catch块能够抓住try块中抛出的ExampleB类型的异常）

面试题 - 说出下面代码的运行结果。（此题的出处是《Java编程思想》一书）

class Annoyance extends Exception {}

class Sneeze extends Annoyance {}

 

class Human {

 

​    public static void main(String[] args) 

​        throws Exception {

​        try {

​            try {

​                throw new Sneeze();

​            } 

​            catch ( Annoyance a ) {

​                System.out.println("Caught Annoyance");

​                throw a;

​            }

​        } 

​        catch ( Sneeze s ) {

​            System.out.println("Caught Sneeze");

​            return ;

​        }

​        finally {

​            System.out.println("Hello World!");

​        }

​    }

}

### List、Set、Map是否继承自Collection接口？ 

答：List、Set 是，Map 不是。Map是键值对映射容器，与List和Set有明显的区别，而Set存储的零散的元素且不允许有重复元素（数学中的集合也是如此），List是线性结构的容器，适用于按数值索引访问元素的情形。

### 阐述ArrayList、Vector、LinkedList的存储性能和特性。 

答：ArrayList 和Vector都是使用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元素，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以索引数据快而插入数据慢，Vector中的方法由于添加了synchronized修饰，因此Vector是线程安全的容器，但性能上较ArrayList差，因此已经是Java中的遗留容器。LinkedList使用双向链表实现存储（将内存中零散的内存单元通过附加的引用关联起来，形成一个可以按序号索引的线性结构，这种链式存储方式与数组的连续存储方式相比，内存的利用率更高），按序号索引数据需要进行前向或后向遍历，但是插入数据时只需要记录本项的前后项即可，所以插入速度较快。Vector属于遗留容器（Java早期的版本中提供的容器，除此之外，Hashtable、Dictionary、BitSet、Stack、Properties都是遗留容器），已经不推荐使用，但是由于ArrayList和LinkedListed都是非线程安全的，如果遇到多个线程操作同一个容器的场景，则可以通过工具类Collections中的synchronizedList方法将其转换成线程安全的容器后再使用（这是对装潢模式的应用，将已有对象传入另一个类的构造器中创建新的对象来增强实现）。

补充：遗留容器中的Properties类和Stack类在设计上有严重的问题，Properties是一个键和值都是字符串的特殊的键值对映射，在设计上应该是关联一个Hashtable并将其两个泛型参数设置为String类型，但是Java API中的Properties直接继承了Hashtable，这很明显是对继承的滥用。这里复用代码的方式应该是Has-A关系而不是Is-A关系，另一方面容器都属于工具类，继承工具类本身就是一个错误的做法，使用工具类最好的方式是Has-A关系（关联）或Use-A关系（依赖）。同理，Stack类继承Vector也是不正确的。Sun公司的工程师们也会犯这种低级错误，让人唏嘘不已。

### Collection和Collections的区别？ 

答：Collection是一个接口，它是Set、List等容器的父接口；Collections是个一个工具类，提供了一系列的静态方法来辅助容器操作，这些方法包括对容器的搜索、排序、线程安全化等等。

### List、Map、Set三个接口存取元素时，各有什么特点？

 答：List以特定索引来存取元素，可以有重复元素。Set不能存放重复元素（用对象的equals()方法来区分元素是否重复）。Map保存键值对（key-value pair）映射，映射关系可以是一对一或多对一。Set和Map容器都有基于哈希存储和排序树的两种实现版本，基于哈希存储的版本理论存取时间复杂度为O(1)，而基于排序树版本的实现在插入或删除元素时会按照元素或元素的键（key）构成排序树从而达到排序和去重的效果。

### TreeMap和TreeSet在排序时如何比较元素？Collections工具类中的sort()方法如何比较元素？ 

答：TreeSet要求存放的对象所属的类必须实现Comparable接口，该接口提供了比较元素的compareTo()方法，当插入元素时会回调该方法比较元素的大小。TreeMap要求存放的键值对映射的键必须实现Comparable接口从而根据键对元素进行排序。Collections工具类的sort方法有两种重载的形式，第一种要求传入的待排序容器中存放的对象比较实现Comparable接口以实现元素的比较；第二种不强制性的要求容器中的元素必须可比较，但是要求传入第二个参数，参数是Comparator接口的子类型（需要重写compare方法实现元素的比较），相当于一个临时定义的排序规则，其实就是通过接口注入比较元素大小的算法，也是对回调模式的应用（Java中对函数式编程的支持）。 
例子1：

 

public class Student implements Comparable<Student> {

​    private String name;        // 姓名

​    private int age;            // 年龄

 

​    public Student(String name, int age) {

​        this.name = name;

​        this.age = age;

​    }

 

​    @Override

​    public String toString() {

​        return "Student [name=" + name + ", age=" + age + "]";

​    }

 

​    @Override

​    public int compareTo(Student o) {

​        return this.age - o.age; // 比较年龄(年龄的升序)

​    }

 

}

import java.util.Set;

import java.util.TreeSet;

 

class Test01 {

 

​    public static void main(String[] args) {

​        Set<Student> set = new TreeSet<>();     // Java 7的钻石语法(构造器后面的尖括号中不需要写类型)

​        set.add(new Student("Hao LUO", 33));

​        set.add(new Student("XJ WANG", 32));

​        set.add(new Student("Bruce LEE", 60));

​        set.add(new Student("Bob YANG", 22));

 

​        for(Student stu : set) {

​            System.out.println(stu);

​        }

//      输出结果: 

//      Student [name=Bob YANG, age=22]

//      Student [name=XJ WANG, age=32]

//      Student [name=Hao LUO, age=33]

//      Student [name=Bruce LEE, age=60]

​    }

}

例子2：

public class Student {

​    private String name;    // 姓名

​    private int age;        // 年龄

 

​    public Student(String name, int age) {

​        this.name = name;

​        this.age = age;

​    }

 

​    /**

​     * 获取学生姓名

​     */

​    public String getName() {

​        return name;

​    }

 

​    /**

​     * 获取学生年龄

​     */

​    public int getAge() {

​        return age;

​    }

 

​    @Override

​    public String toString() {

​        return "Student [name=" + name + ", age=" + age + "]";

​    }

 

}

import java.util.ArrayList;

import java.util.Collections;

import java.util.Comparator;

import java.util.List;

 

class Test02 {

 

​    public static void main(String[] args) {

​        List<Student> list = new ArrayList<>();     // Java 7的钻石语法(构造器后面的尖括号中不需要写类型)

​        list.add(new Student("Hao LUO", 33));

​        list.add(new Student("XJ WANG", 32));

​        list.add(new Student("Bruce LEE", 60));

​        list.add(new Student("Bob YANG", 22));

 

​        // 通过sort方法的第二个参数传入一个Comparator接口对象

​        // 相当于是传入一个比较对象大小的算法到sort方法中

​        // 由于Java中没有函数指针、仿函数、委托这样的概念

​        // 因此要将一个算法传入一个方法中唯一的选择就是通过接口回调

​        Collections.sort(list, new Comparator<Student> () {

 

​            @Override

​            public int compare(Student o1, Student o2) {

​                return o1.getName().compareTo(o2.getName());    // 比较学生姓名

​            }

​        });

 

​        for(Student stu : list) {

​            System.out.println(stu);

​        }

//      输出结果: 

//      Student [name=Bob YANG, age=22]

//      Student [name=Bruce LEE, age=60]

//      Student [name=Hao LUO, age=33]

//      Student [name=XJ WANG, age=32]

​    }

}

### Thread类的sleep()方法和对象的wait()方法都可以让线程暂停执行，它们有什么区别? 

答：sleep()方法（休眠）是线程类（Thread）的静态方法，调用此方法会让当前线程暂停执行指定的时间，将执行机会（CPU）让给其他线程，但是对象的锁依然保持，因此休眠时间结束后会自动恢复（线程回到就绪状态，请参考第66题中的线程状态转换图）。wait()是Object类的方法，调用对象的wait()方法导致当前线程放弃对象的锁（线程暂停执行），进入对象的等待池（wait pool），只有调用对象的notify()方法（或notifyAll()方法）时才能唤醒等待池中的线程进入等锁池（lock pool），如果线程重新获得对象的锁就可以进入就绪状态。

补充：可能不少人对什么是进程，什么是线程还比较模糊，对于为什么需要多线程编程也不是特别理解。简单的说：进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动，是操作系统进行资源分配和调度的一个独立单位；线程是进程的一个实体，是CPU调度和分派的基本单位，是比进程更小的能独立运行的基本单位。线程的划分尺度小于进程，这使得多线程程序的并发性高；进程在执行时通常拥有独立的内存单元，而线程之间可以共享内存。使用多线程的编程通常能够带来更好的性能和用户体验，但是多线程的程序对于其他程序是不友好的，因为它可能占用了更多的CPU资源。当然，也不是线程越多，程序的性能就越好，因为线程之间的调度和切换也会浪费CPU时间。时下很时髦的Node.js就采用了单线程异步I/O的工作模式。

### 线程的sleep()方法和yield()方法有什么区别？ 

答： 
① sleep()方法给其他线程运行机会时不考虑线程的优先级，因此会给低优先级的线程以运行的机会；yield()方法只会给相同优先级或更高优先级的线程以运行的机会； 
② 线程执行sleep()方法后转入阻塞（blocked）状态，而执行yield()方法后转入就绪（ready）状态； 
③ sleep()方法声明抛出InterruptedException，而yield()方法没有声明任何异常； 
④ sleep()方法比yield()方法（跟操作系统CPU调度相关）具有更好的可移植性。

### 当一个线程进入一个对象的synchronized方法A之后，其它线程是否可进入此对象的synchronized方法B？ 

答：不能。其它线程只能访问该对象的非同步方法，同步方法则不能进入。因为非静态方法上的synchronized修饰符要求执行方法时要获得对象的锁，如果已经进入A方法说明对象锁已经被取走，那么试图进入B方法的线程就只能在等锁池（注意不是等待池哦）中等待对象的锁。

### 请说出与线程同步以及线程调度相关的方法。

 答： 
- wait()：使一个线程处于等待（阻塞）状态，并且释放所持有的对象的锁； 
- sleep()：使一个正在运行的线程处于睡眠状态，是一个静态方法，调用此方法要处理InterruptedException异常； 
- notify()：唤醒一个处于等待状态的线程，当然在调用此方法的时候，并不能确切的唤醒某一个等待状态的线程，而是由JVM确定唤醒哪个线程，而且与优先级无关； 
- notityAll()：唤醒所有处于等待状态的线程，该方法并不是将对象的锁给所有线程，而是让它们竞争，只有获得锁的线程才能进入就绪状态；

提示：关于Java多线程和并发编程的问题，建议大家看我的另一篇文章《关于Java并发编程的总结和思考》。

补充：Java 5通过Lock接口提供了显式的锁机制（explicit lock），增强了灵活性以及对线程的协调。Lock接口中定义了加锁（lock()）和解锁（unlock()）的方法，同时还提供了newCondition()方法来产生用于线程之间通信的Condition对象；此外，Java 5还提供了信号量机制（semaphore），信号量可以用来限制对某个共享资源进行访问的线程的数量。在对资源进行访问之前，线程必须得到信号量的许可（调用Semaphore对象的acquire()方法）；在完成对资源的访问后，线程必须向信号量归还许可（调用Semaphore对象的release()方法）。

下面的例子演示了100个线程同时向一个银行账户中存入1元钱，在没有使用同步机制和使用同步机制情况下的执行情况。

银行账户类：

/**

 * 银行账户

 * @author 骆昊

 *

 */

public class Account {

​    private double balance;     // 账户余额

 

​    /**

​     * 存款

​     * @param money 存入金额

​     */

​    public void deposit(double money) {

​        double newBalance = balance + money;

​        try {

​            Thread.sleep(10);   // 模拟此业务需要一段处理时间

​        }

​        catch(InterruptedException ex) {

​            ex.printStackTrace();

​        }

​        balance = newBalance;

​    }

 

​    /**

​     * 获得账户余额

​     */

​    public double getBalance() {

​        return balance;

​    }

}

存钱线程类：

/**

 * 存钱线程

 * @author 骆昊

 *

 */

public class AddMoneyThread implements Runnable {

​    private Account account;    // 存入账户

​    private double money;       // 存入金额

 

​    public AddMoneyThread(Account account, double money) {

​        this.account = account;

​        this.money = money;

​    }

 

​    @Override

​    public void run() {

​        account.deposit(money);

​    }

 

}

测试类：

import java.util.concurrent.ExecutorService;

import java.util.concurrent.Executors;

 

public class Test01 {

 

​    public static void main(String[] args) {

​        Account account = new Account();

​        ExecutorService service = Executors.newFixedThreadPool(100);

 

​        for(int i = 1; i <= 100; i++) {

​            service.execute(new AddMoneyThread(account, 1));

​        }

 

​        service.shutdown();

 

​        while(!service.isTerminated()) {}

 

​        System.out.println("账户余额: " + account.getBalance());

​    }

}

在没有同步的情况下，执行结果通常是显示账户余额在10元以下，出现这种状况的原因是，当一个线程A试图存入1元的时候，另外一个线程B也能够进入存款的方法中，线程B读取到的账户余额仍然是线程A存入1元钱之前的账户余额，因此也是在原来的余额0上面做了加1元的操作，同理线程C也会做类似的事情，所以最后100个线程执行结束时，本来期望账户余额为100元，但实际得到的通常在10元以下（很可能是1元哦）。解决这个问题的办法就是同步，当一个线程对银行账户存钱时，需要将此账户锁定，待其操作完成后才允许其他的线程进行操作，代码有如下几种调整方案：

在银行账户的存款（deposit）方法上同步（synchronized）关键字

/**

 * 银行账户

 * @author 骆昊

 *

 */

public class Account {

​    private double balance;     // 账户余额

 

​    /**

​     * 存款

​     * @param money 存入金额

​     */

​    public synchronized void deposit(double money) {

​        double newBalance = balance + money;

​        try {

​            Thread.sleep(10);   // 模拟此业务需要一段处理时间

​        }

​        catch(InterruptedException ex) {

​            ex.printStackTrace();

​        }

​        balance = newBalance;

​    }

 

​    /**

​     * 获得账户余额

​     */

​    public double getBalance() {

​        return balance;

​    }

}

在线程调用存款方法时对银行账户进行同步

/**

 * 存钱线程

 * @author 骆昊

 *

 */

public class AddMoneyThread implements Runnable {

​    private Account account;    // 存入账户

​    private double money;       // 存入金额

 

​    public AddMoneyThread(Account account, double money) {

​        this.account = account;

​        this.money = money;

​    }

 

​    @Override

​    public void run() {

​        synchronized (account) {

​            account.deposit(money); 

​        }

​    }

 

}

通过Java 5显示的锁机制，为每个银行账户创建一个锁对象，在存款操作进行加锁和解锁的操作

import java.util.concurrent.locks.Lock;

import java.util.concurrent.locks.ReentrantLock;

 

/**

 * 银行账户

 * 

 * @author 骆昊

 *

 */

public class Account {

​    private Lock accountLock = new ReentrantLock();

​    private double balance; // 账户余额

 

​    /**

​     * 存款

​     * 

​     * @param money

​     *            存入金额

​     */

​    public void deposit(double money) {

​        accountLock.lock();

​        try {

​            double newBalance = balance + money;

​            try {

​                Thread.sleep(10); // 模拟此业务需要一段处理时间

​            }

​            catch (InterruptedException ex) {

​                ex.printStackTrace();

​            }

​            balance = newBalance;

​        }

​        finally {

​            accountLock.unlock();

​        }

​    }

 

​    /**

​     * 获得账户余额

​     */

​    public double getBalance() {

​        return balance;

​    }

}

按照上述三种方式对代码进行修改后，重写执行测试代码Test01，将看到最终的账户余额为100元。当然也可以使用Semaphore或CountdownLatch来实现同步。

### 编写多线程程序有几种实现方式？ 

答：Java 5以前实现多线程有两种实现方法：一种是继承Thread类；另一种是实现Runnable接口。两种方式都要通过重写run()方法来定义线程的行为，推荐使用后者，因为Java中的继承是单继承，一个类有一个父类，如果继承了Thread类就无法再继承其他类了，显然使用Runnable接口更为灵活。

补充：Java 5以后创建线程还有第三种方式：实现Callable接口，该接口中的call方法可以在线程执行结束时产生一个返回值，代码如下所示：

import java.util.ArrayList;

import java.util.List;

import java.util.concurrent.Callable;

import java.util.concurrent.ExecutorService;

import java.util.concurrent.Executors;

import java.util.concurrent.Future;

 

 

class MyTask implements Callable<Integer> {

​    private int upperBounds;

 

​    public MyTask(int upperBounds) {

​        this.upperBounds = upperBounds;

​    }

 

​    @Override

​    public Integer call() throws Exception {

​        int sum = 0; 

​        for(int i = 1; i <= upperBounds; i++) {

​            sum += i;

​        }

​        return sum;

​    }

 

}

 

class Test {

 

​    public static void main(String[] args) throws Exception {

​        List<Future<Integer>> list = new ArrayList<>();

​        ExecutorService service = Executors.newFixedThreadPool(10);

​        for(int i = 0; i < 10; i++) {

​            list.add(service.submit(new MyTask((int) (Math.random() * 100))));

​        }

 

​        int sum = 0;

​        for(Future<Integer> future : list) {

​            // while(!future.isDone()) ;

​            sum += future.get();

​        }

 

​        System.out.println(sum);

​    }

}

### synchronized关键字的用法？ 

答：synchronized关键字可以将对象或者方法标记为同步，以实现对对象和方法的互斥访问，可以用synchronized(对象) { … }定义同步代码块，或者在声明方法时将synchronized作为方法的修饰符。在第60题的例子中已经展示了synchronized关键字的用法。

### 举例说明同步和异步。 

答：如果系统中存在临界资源（资源数量少于竞争资源的线程数量的资源），例如正在写的数据以后可能被另一个线程读到，或者正在读的数据可能已经被另一个线程写过了，那么这些数据就必须进行同步存取（数据库操作中的排他锁就是最好的例子）。当应用程序在对象上调用了一个需要花费很长时间来执行的方法，并且不希望让程序等待方法的返回时，就应该使用异步编程，在很多情况下采用异步途径往往更有效率。事实上，所谓的同步就是指阻塞式操作，而异步就是非阻塞式操作。

### 启动一个线程是调用run()还是start()方法？ 

答：启动一个线程是调用start()方法，使线程所代表的虚拟处理机处于可运行状态，这意味着它可以由JVM 调度并执行，这并不意味着线程就会立即运行。run()方法是线程启动后要进行回调（callback）的方法。

### 什么是线程池（thread pool）？

 答：在面向对象编程中，创建和销毁对象是很费时间的，因为创建一个对象要获取内存资源或者其它更多资源。在Java中更是如此，虚拟机将试图跟踪每一个对象，以便能够在对象销毁后进行垃圾回收。所以提高服务程序效率的一个手段就是尽可能减少创建和销毁对象的次数，特别是一些很耗资源的对象创建和销毁，这就是”池化资源”技术产生的原因。线程池顾名思义就是事先创建若干个可执行的线程放入一个池（容器）中，需要的时候从池中获取线程不用自行创建，使用完毕不需要销毁线程而是放回池中，从而减少创建和销毁线程对象的开销。 
Java 5+中的Executor接口定义一个执行线程的工具。它的子类型即线程池接口是ExecutorService。要配置一个线程池是比较复杂的，尤其是对于线程池的原理不是很清楚的情况下，因此在工具类Executors面提供了一些静态工厂方法，生成一些常用的线程池，如下所示： 
- newSingleThreadExecutor：创建一个单线程的线程池。这个线程池只有一个线程在工作，也就是相当于单线程串行执行所有任务。如果这个唯一的线程因为异常结束，那么会有一个新的线程来替代它。此线程池保证所有任务的执行顺序按照任务的提交顺序执行。 
- newFixedThreadPool：创建固定大小的线程池。每次提交一个任务就创建一个线程，直到线程达到线程池的最大大小。线程池的大小一旦达到最大值就会保持不变，如果某个线程因为执行异常而结束，那么线程池会补充一个新线程。 
- newCachedThreadPool：创建一个可缓存的线程池。如果线程池的大小超过了处理任务所需要的线程，那么就会回收部分空闲（60秒不执行任务）的线程，当任务数增加时，此线程池又可以智能的添加新线程来处理任务。此线程池不会对线程池大小做限制，线程池大小完全依赖于操作系统（或者说JVM）能够创建的最大线程大小。 
- newScheduledThreadPool：创建一个大小无限的线程池。此线程池支持定时以及周期性执行任务的需求。 
- newSingleThreadExecutor：创建一个单线程的线程池。此线程池支持定时以及周期性执行任务的需求。

第60题的例子中演示了通过Executors工具类创建线程池并使用线程池执行线程的代码。如果希望在服务器上使用线程池，强烈建议使用newFixedThreadPool方法来创建线程池，这样能获得更好的性能。

### 线程的基本状态以及状态之间的关系？ 

答： 

说明：其中Running表示运行状态，Runnable表示就绪状态（万事俱备，只欠CPU），Blocked表示阻塞状态，阻塞状态又有多种情况，可能是因为调用wait()方法进入等待池，也可能是执行同步方法或同步代码块进入等锁池，或者是调用了sleep()方法或join()方法等待休眠或其他线程结束，或是因为发生了I/O中断。

### 简述synchronized 和java.util.concurrent.locks.Lock的异同？

答：Lock是Java 5以后引入的新的API，和关键字synchronized相比主要相同点：Lock 能完成synchronized所实现的所有功能；主要不同点：Lock有比synchronized更精确的线程语义和更好的性能，而且不强制性的要求一定要获得锁。synchronized会自动释放锁，而Lock一定要求程序员手工释放，并且最好在finally 块中释放（这是释放外部资源的最好的地方）。

### Java中如何实现序列化，有什么意义？ 

答：序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决对象流读写操作时可能引发的问题（如果不进行序列化可能会存在数据乱序的问题）。 
要实现序列化，需要让一个类实现Serializable接口，该接口是一个标识性接口，标注该类对象是可被序列化的，然后使用一个输出流来构造一个对象输出流并通过writeObject(Object)方法就可以将实现对象写出（即保存其状态）；如果需要反序列化则可以用一个输入流建立对象输入流，然后通过readObject方法从流中读取对象。序列化除了能够实现对象的持久化之外，还能够用于对象的深度克隆（可以参考第29题）。

### Java中有几种类型的流？

 答：字节流和字符流。字节流继承于InputStream、OutputStream，字符流继承于Reader、Writer。在java.io 包中还有许多其他的流，主要是为了提高性能和使用方便。关于Java的I/O需要注意的有两点：一是两种对称性（输入和输出的对称性，字节和字符的对称性）；二是两种设计模式（适配器模式和装潢模式）。另外Java中的流不同于C#的是它只有一个维度一个方向。

面试题 - 编程实现文件拷贝。（这个题目在笔试的时候经常出现，下面的代码给出了两种实现方案）

import java.io.FileInputStream;

import java.io.FileOutputStream;

import java.io.IOException;

import java.io.InputStream;

import java.io.OutputStream;

import java.nio.ByteBuffer;

import java.nio.channels.FileChannel;

 

public final class MyUtil {

 

​    private MyUtil() {

​        throw new AssertionError();

​    }

 

​    public static void fileCopy(String source, String target) throws IOException {

​        try (InputStream in = new FileInputStream(source)) {

​            try (OutputStream out = new FileOutputStream(target)) {

​                byte[] buffer = new byte[4096];

​                int bytesToRead;

​                while((bytesToRead = in.read(buffer)) != -1) {

​                    out.write(buffer, 0, bytesToRead);

​                }

​            }

​        }

​    }

 

​    public static void fileCopyNIO(String source, String target) throws IOException {

​        try (FileInputStream in = new FileInputStream(source)) {

​            try (FileOutputStream out = new FileOutputStream(target)) {

​                FileChannel inChannel = in.getChannel();

​                FileChannel outChannel = out.getChannel();

​                ByteBuffer buffer = ByteBuffer.allocate(4096);

​                while(inChannel.read(buffer) != -1) {

​                    buffer.flip();

​                    outChannel.write(buffer);

​                    buffer.clear();

​                }

​            }

​        }

​    }

}

注意：上面用到Java 7的TWR，使用TWR后可以不用在finally中释放外部资源 ，从而让代码更加优雅。

### 写一个方法，输入一个文件名和一个字符串，统计这个字符串在这个文件中出现的次数。


答：代码如下：

import java.io.BufferedReader;

import java.io.FileReader;

 

public final class MyUtil {

 

​    // 工具类中的方法都是静态方式访问的因此将构造器私有不允许创建对象(绝对好习惯)

​    private MyUtil() {

​        throw new AssertionError();

​    }

 

​    /**

​     * 统计给定文件中给定字符串的出现次数

​     * 

​     * @param filename  文件名

​     * @param word 字符串

​     * @return 字符串在文件中出现的次数

​     */

​    public static int countWordInFile(String filename, String word) {

​        int counter = 0;

​        try (FileReader fr = new FileReader(filename)) {

​            try (BufferedReader br = new BufferedReader(fr)) {

​                String line = null;

​                while ((line = br.readLine()) != null) {

​                    int index = -1;

​                    while (line.length() >= word.length() && (index = line.indexOf(word)) >= 0) {

​                        counter++;

​                        line = line.substring(index + word.length());

​                    }

​                }

​            }

​        } catch (Exception ex) {

​            ex.printStackTrace();

​        }

​        return counter;

​    }

 

}

### 如何用Java代码列出一个目录下所有的文件？ 

答： 
如果只要求列出当前文件夹下的文件，代码如下所示：

import java.io.File;

 

class Test12 {

 

​    public static void main(String[] args) {

​        File f = new File("/Users/Hao/Downloads");

​        for(File temp : f.listFiles()) {

​            if(temp.isFile()) {

​                System.out.println(temp.getName());

​            }

​        }

​    }

}

如果需要对文件夹继续展开，代码如下所示：

import java.io.File;

 

class Test12 {

 

​    public static void main(String[] args) {

​        showDirectory(new File("/Users/Hao/Downloads"));

​    }

 

​    public static void showDirectory(File f) {

​        _walkDirectory(f, 0);

​    }

 

​    private static void _walkDirectory(File f, int level) {

​        if(f.isDirectory()) {

​            for(File temp : f.listFiles()) {

​                _walkDirectory(temp, level + 1);

​            }

​        }

​        else {

​            for(int i = 0; i < level - 1; i++) {

​                System.out.print("\t");

​            }

​            System.out.println(f.getName());

​        }

​    }

}

在Java 7中可以使用NIO.2的API来做同样的事情，代码如下所示：

class ShowFileTest {

 

​    public static void main(String[] args) throws IOException {

​        Path initPath = Paths.get("/Users/Hao/Downloads");

​        Files.walkFileTree(initPath, new SimpleFileVisitor<Path>() {

 

​            @Override

​            public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) 

​                    throws IOException {

​                System.out.println(file.getFileName().toString());

​                return FileVisitResult.CONTINUE;

​            }

 

​        });

​    }

}

### 用Java的套接字编程实现一个多线程的回显（echo）服务器。

 答：

import java.io.BufferedReader;

import java.io.IOException;

import java.io.InputStreamReader;

import java.io.PrintWriter;

import java.net.ServerSocket;

import java.net.Socket;

 

public class EchoServer {

 

​    private static final int ECHO_SERVER_PORT = 6789;

 

​    public static void main(String[] args) {        

​        try(ServerSocket server = new ServerSocket(ECHO_SERVER_PORT)) {

​            System.out.println("服务器已经启动...");

​            while(true) {

​                Socket client = server.accept();

​                new Thread(new ClientHandler(client)).start();

​            }

​        } catch (IOException e) {

​            e.printStackTrace();

​        }

​    }

 

​    private static class ClientHandler implements Runnable {

​        private Socket client;

 

​        public ClientHandler(Socket client) {

​            this.client = client;

​        }

 

​        @Override

​        public void run() {

​            try(BufferedReader br = new BufferedReader(new InputStreamReader(client.getInputStream()));

​                    PrintWriter pw = new PrintWriter(client.getOutputStream())) {

​                String msg = br.readLine();

​                System.out.println("收到" + client.getInetAddress() + "发送的: " + msg);

​                pw.println(msg);

​                pw.flush();

​            } catch(Exception ex) {

​                ex.printStackTrace();

​            } finally {

​                try {

​                    client.close();

​                } catch (IOException e) {

​                    e.printStackTrace();

​                }

​            }

​        }

​    }

 

}

注意：上面的代码使用了Java 7的TWR语法，由于很多外部资源类都间接的实现了AutoCloseable接口（单方法回调接口），因此可以利用TWR语法在try结束的时候通过回调的方式自动调用外部资源类的close()方法，避免书写冗长的finally代码块。此外，上面的代码用一个静态内部类实现线程的功能，使用多线程可以避免一个用户I/O操作所产生的中断影响其他用户对服务器的访问，简单的说就是一个用户的输入操作不会造成其他用户的阻塞。当然，上面的代码使用线程池可以获得更好的性能，因为频繁的创建和销毁线程所造成的开销也是不可忽视的。

下面是一段回显客户端测试代码：

import java.io.BufferedReader;

import java.io.InputStreamReader;

import java.io.PrintWriter;

import java.net.Socket;

import java.util.Scanner;

 

public class EchoClient {

 

​    public static void main(String[] args) throws Exception {

​        Socket client = new Socket("localhost", 6789);

​        Scanner sc = new Scanner(System.in);

​        System.out.print("请输入内容: ");

​        String msg = sc.nextLine();

​        sc.close();

​        PrintWriter pw = new PrintWriter(client.getOutputStream());

​        pw.println(msg);

​        pw.flush();

​        BufferedReader br = new BufferedReader(new InputStreamReader(client.getInputStream()));

​        System.out.println(br.readLine());

​        client.close();

​    }

}

如果希望用NIO的多路复用套接字实现服务器，代码如下所示。NIO的操作虽然带来了更好的性能，但是有些操作是比较底层的，对于初学者来说还是有些难于理解。

import java.io.IOException;

import java.net.InetSocketAddress;

import java.nio.ByteBuffer;

import java.nio.CharBuffer;

import java.nio.channels.SelectionKey;

import java.nio.channels.Selector;

import java.nio.channels.ServerSocketChannel;

import java.nio.channels.SocketChannel;

import java.util.Iterator;

 

public class EchoServerNIO {

 

​    private static final int ECHO_SERVER_PORT = 6789;

​    private static final int ECHO_SERVER_TIMEOUT = 5000;

​    private static final int BUFFER_SIZE = 1024;

 

​    private static ServerSocketChannel serverChannel = null;

​    private static Selector selector = null;    // 多路复用选择器

​    private static ByteBuffer buffer = null;    // 缓冲区

 

​    public static void main(String[] args) {

​        init();

​        listen();

​    }

 

​    private static void init() {

​        try {

​            serverChannel = ServerSocketChannel.open();

​            buffer = ByteBuffer.allocate(BUFFER_SIZE);

​            serverChannel.socket().bind(new InetSocketAddress(ECHO_SERVER_PORT));

​            serverChannel.configureBlocking(false);

​            selector = Selector.open();

​            serverChannel.register(selector, SelectionKey.OP_ACCEPT);

​        } catch (Exception e) {

​            throw new RuntimeException(e);

​        }

​    }

 

​    private static void listen() {

​        while (true) {

​            try {

​                if (selector.select(ECHO_SERVER_TIMEOUT) != 0) {

​                    Iterator<SelectionKey> it = selector.selectedKeys().iterator();

​                    while (it.hasNext()) {

​                        SelectionKey key = it.next();

​                        it.remove();

​                        handleKey(key);

​                    }

​                }

​            } catch (Exception e) {

​                e.printStackTrace();

​            }

​        }

​    }

 

​    private static void handleKey(SelectionKey key) throws IOException {

​        SocketChannel channel = null;

 

​        try {

​            if (key.isAcceptable()) {

​                ServerSocketChannel serverChannel = (ServerSocketChannel) key.channel();

​                channel = serverChannel.accept();

​                channel.configureBlocking(false);

​                channel.register(selector, SelectionKey.OP_READ);

​            } else if (key.isReadable()) {

​                channel = (SocketChannel) key.channel();

​                buffer.clear();

​                if (channel.read(buffer) > 0) {

​                    buffer.flip();

​                    CharBuffer charBuffer = CharsetHelper.decode(buffer);

​                    String msg = charBuffer.toString();

​                    System.out.println("收到" + channel.getRemoteAddress() + "的消息：" + msg);

​                    channel.write(CharsetHelper.encode(CharBuffer.wrap(msg)));

​                } else {

​                    channel.close();

​                }

​            }

​        } catch (Exception e) {

​            e.printStackTrace();

​            if (channel != null) {

​                channel.close();

​            }

​        }

​    }

 

}

import java.nio.ByteBuffer;

import java.nio.CharBuffer;

import java.nio.charset.CharacterCodingException;

import java.nio.charset.Charset;

import java.nio.charset.CharsetDecoder;

import java.nio.charset.CharsetEncoder;

 

public final class CharsetHelper {

​    private static final String UTF_8 = "UTF-8";

​    private static CharsetEncoder encoder = Charset.forName(UTF_8).newEncoder();

​    private static CharsetDecoder decoder = Charset.forName(UTF_8).newDecoder();

 

​    private CharsetHelper() {

​    }

 

​    public static ByteBuffer encode(CharBuffer in) throws CharacterCodingException{

​        return encoder.encode(in);

​    }

 

​    public static CharBuffer decode(ByteBuffer in) throws CharacterCodingException{

​        return decoder.decode(in);

​    }

}

### XML文档定义有几种形式？它们之间有何本质区别？解析XML文档有哪几种方式？ 

答：XML文档定义分为DTD和Schema两种形式，二者都是对XML语法的约束，其本质区别在于Schema本身也是一个XML文件，可以被XML解析器解析，而且可以为XML承载的数据定义类型，约束能力较之DTD更强大。对XML的解析主要有DOM（文档对象模型，Document Object Model）、SAX（Simple API for XML）和StAX（Java 6中引入的新的解析XML的方式，Streaming API for XML），其中DOM处理大型文件时其性能下降的非常厉害，这个问题是由DOM树结构占用的内存较多造成的，而且DOM解析方式必须在解析文件之前把整个文档装入内存，适合对XML的随机访问（典型的用空间换取时间的策略）；SAX是事件驱动型的XML解析方式，它顺序读取XML文件，不需要一次全部装载整个文件。当遇到像文件开头，文档结束，或者标签开头与标签结束时，它会触发一个事件，用户通过事件回调代码来处理XML文件，适合对XML的顺序访问；顾名思义，StAX把重点放在流上，实际上StAX与其他解析方式的本质区别就在于应用程序能够把XML作为一个事件流来处理。将XML作为一组事件来处理的想法并不新颖（SAX就是这样做的），但不同之处在于StAX允许应用程序代码把这些事件逐个拉出来，而不用提供在解析器方便时从解析器中接收事件的处理程序。

### 你在项目中哪些地方用到了XML？

 答：XML的主要作用有两个方面：数据交换和信息配置。在做数据交换时，XML将数据用标签组装成起来，然后压缩打包加密后通过网络传送给接收者，接收解密与解压缩后再从XML文件中还原相关信息进行处理，XML曾经是异构系统间交换数据的事实标准，但此项功能几乎已经被JSON（JavaScript Object Notation）取而代之。当然，目前很多软件仍然使用XML来存储配置信息，我们在很多项目中通常也会将作为配置信息的硬代码写在XML文件中，Java的很多框架也是这么做的，而且这些框架都选择了dom4j作为处理XML的工具，因为Sun公司的官方API实在不怎么好用。

补充：现在有很多时髦的软件（如Sublime）已经开始将配置文件书写成JSON格式，我们已经强烈的感受到XML的另一项功能也将逐渐被业界抛弃。

 





 





 





 

## UML

### 什么是UML？ 

答：UML是统一建模语言（Unified Modeling Language）的缩写，它发表于1997年，综合了当时已经存在的面向对象的建模语言、方法和过程，是一个支持模型化和软件系统开发的图形化语言，为软件开发的所有阶段提供模型化和可视化支持。使用UML可以帮助沟通与交流，辅助应用设计和文档的生成，还能够阐释系统的结构和行为。

### UML中有哪些常用的图？ 

答：UML定义了多种图形化的符号来描述软件系统部分或全部的静态结构和动态结构，包括：用例图（use case diagram）、类图（class diagram）、时序图（sequence diagram）、协作图（collaboration diagram）、状态图（statechart diagram）、活动图（activity diagram）、构件图（component diagram）、部署图（deployment diagram）等。在这些图形化符号中，有三种图最为重要，分别是：用例图（用来捕获需求，描述系统的功能，通过该图可以迅速的了解系统的功能模块及其关系）、类图（描述类以及类与类之间的关系，通过该图可以快速了解系统）、时序图（描述执行特定任务时对象之间的交互关系以及执行顺序，通过该图可以了解对象能接收的消息也就是说对象能够向外界提供的服务）。 

用例图：  
类图：  
时序图： 



 

## RMI（远程方法调用）

### 什么是RMI？

Java远程方法调用(Java RMI)是Java API对远程过程调用(RPC)提供的面向对象的等价形式，支持直接传输序列化的Java对象和分布式垃圾回收。远程方法调用可以看做是激活远程正在运行的对象上的方法的步骤。RMI对调用者是位置透明的，因为调用者感觉方法是执行在本地运行的对象上的。看下RMI的一些注意事项。

### RMI体系结构的基本原则是什么？

RMI体系结构是基于一个非常重要的行为定义和行为实现相分离的原则。RMI允许定义行为的代码和实现行为的代码相分离，并且运行在不同的JVM上。

### RMI体系结构分哪几层？

RMI体系结构分以下几层：

存根和骨架层(Stub and Skeleton layer)：这一层对程序员是透明的，它主要负责拦截客户端发出的方法调用请求，然后把请求重定向给远程的RMI服务。

远程引用层(Remote Reference Layer)：RMI体系结构的第二层用来解析客户端对服务端远程对象的引用。这一层解析并管理客户端对服务端远程对象的引用。连接是点到点的。

传输层(Transport layer)：这一层负责连接参与服务的两个JVM。这一层是建立在网络上机器间的TCP/IP连接之上的。它提供了基本的连接服务，还有一些防火墙穿透策略。

### RMI中的远程接口(Remote Interface)扮演了什么样的角色？

远程接口用来标识哪些方法是可以被非本地虚拟机调用的接口。远程对象必须要直接或者是间接实现远程接口。实现了远程接口的类应该声明被实现的远程接口，给每一个远程对象定义构造函数，给所有远程接口的方法提供实现。

### java.rmi.Naming类扮演了什么样的角色？

java.rmi.Naming类用来存储和获取在远程对象注册表里面的远程对象的引用。Naming类的每一个方法接收一个URL格式的String对象作为它的参数。

### RMI的绑定(Binding)是什么意思？

绑定是为了查询找远程对象而给远程对象关联或者是注册以后会用到的名称的过程。远程对象可以使用Naming类的bind()或者rebind()方法跟名称相关联。

### Naming类的bind()和rebind()方法有什么区别？

bind()方法负责把指定名称绑定给远程对象，rebind()方法负责把指定名称重新绑定到一个新的远程对象。如果那个名称已经绑定过了，先前的绑定会被替换掉。

### 让RMI程序能正确运行有哪些步骤？

为了让RMI程序能正确运行必须要包含以下几个步骤：

编译所有的源文件。

使用rmic生成stub。

启动rmiregistry。

启动RMI服务器。

运行客户端程序。

### RMI的stub扮演了什么样的角色？

远程对象的stub扮演了远程对象的代表或者代理的角色。调用者在本地stub上调用方法，它负责在远程对象上执行方法。当stub的方法被调用的时候，会经历以下几个步骤：

初始化到包含了远程对象的JVM的连接。

序列化参数到远程的JVM。

等待方法调用和执行的结果。

反序列化返回的值或者是方法没有执行成功情况下的异常。

把值返回给调用者。

### 什么是分布式垃圾回收(DGC)？它是如何工作的？

DGC叫做分布式垃圾回收。RMI使用DGC来做自动垃圾回收。因为RMI包含了跨虚拟机的远程对象的引用，垃圾回收是很困难的。DGC使用引用计数算法来给远程对象提供自动内存管理。

### RMI中使用RMI安全管理器(RMISecurityManager)的目的是什么？

RMISecurityManager使用下载好的代码提供可被RMI应用程序使用的安全管理器。如果没有设置安全管理器，RMI的类加载器就不会从远程下载任何的类。

 

 



 

## Object类

### Object 类中有哪些方法？作用是什么？

在 object 类中有 11 个方法，分别是：

clone() //创建并返回此对象的副本

equals(Object obj) //指示一些其他对象是否等于此。

finalize() //当垃圾收集确定不再有对该对象的引用时，垃圾收集器在对象上调用该对象。

getClass() //返回此 Object的运行时类。

hashCode() //返回对象的哈希码值。

notify() //唤醒正在等待对象监视器的单个线程。

notifyAll() //唤醒正在等待对象监视器的所有线程。

toString() //返回对象的字符串表示形式。

wait()	//导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 				notifyAll()方法。

wait(long timeout) //导致当前线程等待，直到另一个线程调用 notify()方法或该对象的 notifyAll()方法，或者指定的时间已过。

wait(long timeout, int nanos) //导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 notifyAll()方法，或者某些其他线程中断当前线程，或一定量的实时时间。

 



 

 

 







 

 

### 

### 





### 