官方文档地址：https://docs.oracle.com/javase/7/docs/api/java/io/File.html

Java文件类以抽象的方式代表文件名和目录路径名。该类主要用于文件和目录的创建、文件的查找和文件的删除等。

File对象代表磁盘中实际存在的文件和目录。

```
通过以下构造方法创建一个File对象。
	1. 通过给定的父抽象路径名和子路径名字符串创建一个新的File实例。
    	File(File parent, String child);
	2. 通过将给定路径名字符串转换成抽象路径名来创建一个新 File 实例。
    	File(String pathname) 
	3. 根据 parent 路径名字符串和 child 路径名字符串创建一个新 File 实例。
    	File(String parent, String child) 
	4. 通过将给定的 file: URI 转换成一个抽象路径名来创建一个新的 File 实例。
    	File(URI uri) 
```

#### 操作文件相关的方法

```
public String getName()
	描述：返回由此抽象路径名表示的文件或目录的名称。
public String getParent()
	描述：返回此抽象路径名的父路径名的路径名字符串，如果此路径名没有指定父目录，则返回 null。
public File getParentFile()
	描述：返回此抽象路径名的父路径名的抽象路径名，如果此路径名没有指定父目录，则返回 null。
public String getPath()
	描述：将此抽象路径名转换为一个路径名字符串。
public boolean isAbsolute()
	描述：测试此抽象路径名是否为绝对路径名。
public String getAbsolutePath()
	描述：返回抽象路径名的绝对路径名字符串。
public boolean canRead()
	描述：测试应用程序是否可以读取此抽象路径名表示的文件。
public boolean canWrite()
	描述：测试应用程序是否可以修改此抽象路径名表示的文件。
public boolean exists()
	描述：测试此抽象路径名表示的文件或目录是否存在。
public boolean isDirectory()
	描述：测试此抽象路径名表示的文件是否是一个目录。
public boolean isFile()
	描述：测试此抽象路径名表示的文件是否是一个标准文件。
public long lastModified()
	描述：返回此抽象路径名表示的文件最后一次被修改的时间。
public long length()
	描述：返回由此抽象路径名表示的文件的长度。
public boolean createNewFile() throws IOException
	描述：当且仅当不存在具有此抽象路径名指定的名称的文件时，
		原子地创建由此抽象路径名指定的一个新的空文件。
public boolean delete() 
	描述：删除此抽象路径名表示的文件或目录。
public void deleteOnExit()
	描述：在虚拟机终止时，请求删除此抽象路径名表示的文件或目录。
public String[] list()
	描述：返回由此抽象路径名所表示的目录中的文件和目录的名称所组成字符串数组。
public String[] list(FilenameFilter filter)
	描述：返回由包含在目录中的文件和目录的名称所组成的字符串数组，
	这一目录是通过满足指定过滤器的抽象路径名来表示的。
public File[] listFiles() 
	描述：返回一个抽象路径名数组，这些路径名表示此抽象路径名所表示目录中的文件。
public File[] listFiles(FileFilter filter)
	描述：返回表示此抽象路径名所表示目录中的文件和目录的抽象路径名数组，这些路径名满足特定过滤器。
public boolean mkdir()
	描述：创建此抽象路径名指定的目录。
public boolean mkdirs()
	描述：创建此抽象路径名指定的目录，包括创建必需但不存在的父目录。
public boolean renameTo(File dest) 
	描述：重新命名此抽象路径名表示的文件。
public boolean setLastModified(long time)
	描述：设置由此抽象路径名所指定的文件或目录的最后一次修改时间。
public boolean setReadOnly()
	描述：标记此抽象路径名指定的文件或目录，以便只可对其进行读操作。
public static File createTempFile(String prefix, String suffix, File directory) throws IOException
	描述：在指定目录中创建一个新的空文件，使用给定的前缀和后缀字符串生成其名称。
public static File createTempFile(String prefix, String suffix) throws IOException
	描述：在默认临时文件目录中创建一个空文件，使用给定前缀和后缀生成其名称。
public int compareTo(File pathname)
	描述：按字母顺序比较两个抽象路径名。
public int compareTo(Object o)
	描述：按字母顺序比较抽象路径名与给定对象。
public boolean equals(Object obj)
	描述：测试此抽象路径名与给定对象是否相等。
public String toString() 
	描述：返回此抽象路径名的路径名字符串。
```

#### 实例

下面的实例演示了File对象的使用：

```
import java.io.File;
public class DirList {
   public static void main(String args[]) {
      String dirname = "/java";
      File f1 = new File(dirname);
      if (f1.isDirectory()) {
         System.out.println( "Directory of " + dirname);
         String s[] = f1.list();
         for (int i=0; i < s.length; i++) {
            File f = new File(dirname + "/" + s[i]);
            if (f.isDirectory()) {
               System.out.println(s[i] + " is a directory");
            } else {
               System.out.println(s[i] + " is a file");
            }
         }
      } else {
         System.out.println(dirname + " is not a directory");
    }
  }
}
结果：
Directory of /mysql
bin is a directory
lib is a directory
demo is a directory
test.txt is a file
README is a file
index.html is a file
include is a directory
```

#### 相关面试题

```
下列叙述中，错误的是（ B ）
    A. File类能够存储文件属性
    B. File类能够读写文件
    C. File类能够建立文件
    D. File类能够获取文件目录信息
    解析：
    	File类用于文件和目录的创建，文件的查找和删除，不能够读写文件。
    	
```



