Java 提供了 String 类来创建和操作字符串。

#### 常用方法

```
1. subString() 方法：返回字符串的子串
	格式：
		public String substring(int beginIndex)
		截取从下标为beginIndex起（包括该字符）之后所有字符。
		public String substring(int beginIndex, int endIndex)
		截取 [beginIndex, endIndex)
```

#### 相关面试题

##### 1. java中 String str = "hello world"下列语句错误的是？()

```
A. str+='  a'
B. int strlen = str.length
C. str=100
D. str=str+100
```

```
解析：答案：A,B,C
    A. 单个字符用单引号表示，字符串（多个字符）用双引号表示。
    B. length属性指的是数组的长度，length()方法才是求字符串的长度
    C. int 不能转换成 String
    D. 好像涉及到自动装箱和拆箱机制，反正是对的
```

##### 2. 下面哪段程序能够正确的实现了GBK编码字节流到UTF-8编码字节流的转换：（ ）

```
 byte[] src,dst;

A. dst=String.fromBytes(src，"GBK").getBytes("UTF-8")
B. dst=new String(src，"GBK").getBytes("UTF-8")
C. dst=new String("GBK"，src).getBytes()
D. dst=String.encode(String.decode(src，"GBK"))，"UTF-8" )
```

```
解析：答案：B
    操作步骤就是先解码再编码
    用new String(src，"GBK")解码得到字符串
    用getBytes("UTF-8")得到UTF8编码字节数组
```

##### 3. 顺序执行下列程序语句后，则b的值是（ ）

```
String a="Hello";
String b=a.substring(0,2);

A. Hello
B. Hel
C. He
D. null
```

```
解析：答案：C
	截取的字符串为 [0, 2)
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79837211