java中的String类是按照unicode进行编码的。

#### 相关面试题

```
1. 在Java语言中，下列关于字符集编码（Character set encoding）和国际化（i18n）的问题，哪些是正确的？
    A. 每个中文字符占用2个字节，每个英文字符占用1个字节
    B. 假设数据库中的字符是以GBK编码的，那么显示数据库数据的网页也必须是GBK编码的。
    C. Java的char类型，通常以UTF-16 Big Endian的方式保存一个字符。
    D. 实现国际化应用常用的手段是利用ResourceBundle类
    解析：
    	A 显然是错误的，Java一律采用Unicode编码方式，每个字符无论中文还是英文字符都占用2个字节。
        B 也是不正确的，不同的编码之间是可以转换的，通常流程如下：
        将字符串S以其自身编码方式分解为字节数组，再将字节数组以你想要输出的编码方式重新编码为字符串。
        例：String newUTF8Str = new String(oldGBKStr.getBytes("GBK"), "UTF8");
        C 是正确的。Java虚拟机中通常使用UTF-16的方式保存一个字符
        D 也是正确的。ResourceBundle能够依据Local的不同，选择性的读取与Local对应后缀的properties文件，以达到国际化的目的。
2. 下面哪段程序能够正确的实现了GBK编码字节流到UTF-8编码字节流的转换：（B）
    byte[] src,dst;

    A. dst=String.fromBytes(src，"GBK").getBytes("UTF-8")
    B. dst=new String(src，"GBK").getBytes("UTF-8")
    C. dst=new String("GBK"，src).getBytes()
    D. dst=String.encode(String.decode(src，"GBK"))，"UTF-8" )
    解析：
    	操作步骤就是先解码再编码
          用new String(src，"GBK")解码得到字符串
          用getBytes("UTF-8")得到UTF8编码字节数组
```

