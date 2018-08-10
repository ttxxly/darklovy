Java 语言是面向对象的程序设计语言，Java 程序的基本组成单元是类类体中又包括属性与方法两部分。

每一个应用程序都必须包含一个 `main()` 方法，含有 `main()`方法的类被称为主类。

```
package com.darklovy.Number;

public class First {
    private static String s1 = "你好";

    public static void main(String[] args) {
        String s2 = "Java";
        //测试
        System.out.println(s1);
        System.out.println(s2);
    }
}

运行结果：
你好
Java
```

### 包声明

一个 Java 应用程序是由若干个类组成的，在上面的例子中 `package com.darklovy.Number;` 声明该类所在的包。`package`为包的关键字。

### 声明成员变量和局部变量

* 全局变量：通常将类的属性成为类的全局变量
* 局部变量：方法中的属性成为局部变量。

全局变量声明在类体中，局部变量声明在方法体中，全局变量和局部变量都有各自的生命周期或者说是应用范围

### 编写主方法

`main()`方法是类体中的主方法。该方法从 `{` 到 `}` 结束。`public static void`分别是 `main()`方法的权限修饰符、静态修饰符和返回值修饰符。

Java 程序中的 `main()`方法必须声明为 `public static void`

`Stirng[] args`是一个字符串类型的数组，它是 `main()`方法的参数。`main()`方法是程序开始执行的位置。

### 导入 API 类库

在 Java 语言中可以通过 `import`关键字导入相关的库。

**Java 语言是严格区分大小写的。例如，不能将关键字 class 等同于 Class**



感兴趣的话可以点击下面的链接，关注我的微信公众号和我的知识星球。

> https://www.ttxxly.top/images/qrcode_darklovy.jpg
>
> https://www.ttxxly.top/images/qrcode_ttxxly123.jpg
>
> https://www.ttxxly.top/images/ZSXQ_darklovy.png

发表地址

* [我的博客](https://www.ttxxly.top/2018/08/06/Java-%E4%B8%BB%E7%B1%BB%E7%BB%93%E6%9E%84/)

