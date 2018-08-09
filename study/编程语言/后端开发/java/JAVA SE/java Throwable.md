官方地址：https://docs.oracle.com/javase/7/docs/api/java/lang/Throwable.html

[Razertory](https://www.nowcoder.com/profile/140047)

ABC

 ![](http://uploadfiles.nowcoder.net/images/20151113/140047_1447376765880_373DC390B08E99ABC340DB1F78F35FCB)

```
1.Exception（异常） :是程序本身可以处理的异常。 
2.Error（错误）: 是程序无法处理的错误。这些错误表示故障发生于虚拟机自身、或者发生在虚拟机试图执行应用时，一般不需要程序处理。
3.检查异常（编译器要求必须处置的异常） ：  除了Error，RuntimeException及其子类以外，其他的Exception类及其子类都属于可查异常。这种异常的特点是Java编译器会检查它，也就是说，当程序中可能出现这类异常，要么用try-catch语句捕获它，要么用throws子句声明抛出它，否则编译不会通过。

4.非检查异常(编译器不要求处置的异常): 包括运行时异常（RuntimeException与其子类）和错误（Error）。
```

