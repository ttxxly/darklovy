Java的关键字对Java的编译器有特殊的意义，他们用来表示一种数据类型，或者表示程序的结构等，关键字不能用作变量名、方法名、类名、包名和参数。

#### 关键字列表

```
https://docs.oracle.com/javase/specs/jls/se8/html/jls-3.html#jls-3.9

abstract   continue   for          new         switch
assert     default    if           package     synchronized
boolean    do         goto         private     this
break      double     implements   protected   throw
byte       else       import       public      throws
case       enum       instanceof   return      transient
catch      extends    int          short       try
char       final      interface    static      void
class      finally    long         strictfp    volatile
const      float      native       super       while

The keywords const and goto are reserved, 
even though they are not currently used. 
This may allow a Java compiler to produce better 
error messages if these C++ keywords
incorrectly appear in programs.

While true and false might appear to be keywords,
they are technically boolean literals (§3.10.3).
Similarly, while null might appear to be a keyword,
it is technically the null literal (§3.10.7).
```

#### 相关面试题 

```
1. true、false、null、sizeof、goto、synchronized 哪些是Java关键字？(E,F)
    A true
    B false
    C null
    D sizeof
    E goto
    F synchronized
2. 以下为java语法保留不能作为类名和方法名使用的是（A,B,C,D）
	A default
    B int
    C implements
    D throws
    
```

