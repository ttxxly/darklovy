#### 字符流和字节流的区别

```
字节流操作的基本单元为字节；字符流操作的基本单元为Unicode码元。
字节流默认不使用缓冲区；字符流使用缓冲区。
字节流通常用于处理二进制数据，实际上它可以处理任意类型的数据，但它不支持直接写入或读取Unicode码元；字符流通常处理文本数据，它支持写入及读取Unicode码元。
```

#### 结构图

```
字节流：
InputStream   
|-- FileInputStream (基本文件流）   
|-- BufferedInputStream   
|-- DataInputStream   
|-- ObjectInputStream

字符流
Reader 
|-- InputStreamReader (byte->char 桥梁） 
|-- BufferedReader (常用） 
Writer 
|-- OutputStreamWriter (char->byte 桥梁） 
|-- BufferedWriter 
|-- PrintWriter （常用）
```

