一些关于try catch 简单总结。

```
return：
	在 try、catch语句块中：
		return 如果执行，需要先执行 finally 语句块（如果有），在返回值（方法值）
	在 finally 语句块中
		return 如果执行，将结束这个方法，直接返回值（方法值）（不会再跳回到 try、catch 语句块中）。
System.exit()
	如果执行，将会结束和终止整个程序（注意是整个程序）。
```

#### 相关面试题

```
1. 下面程序的输出是什么？（B）
	package algorithms.com.guan.javajicu;
    public class TestDemo
    {
        public static String output = ””;
        public static void foo(inti)
        {
            try
            {
                if (i == 1)
                {
                    throw new Exception();
                }
            }
            catch (Exception e)
            {
                output += “2”;
                return ;
            } finally
            {
                output += “3”;
            }
            output += “4”;
        }
        public static void main(String[] args)
        {
            foo(0);
            foo(1);
            System.out.println(output);
        }
    }
    A. 342
    B. 3423
    C. 34234
    D. 323
    解析：
    	这道题考察了 return 在 catch语句块中的情况。
    	return 如果执行，需要先执行 finally 语句块（如果有），再返回值（方法值）
    	return 执行完即结束。
2. 执行下列代码的输出结果是（C）
    public class Demo{
     public static void main(String args[]){
       int num = 10;
       System.out.println(test(num));
    }
    public static int test(int b){
       try
       {
        b += 10;
        return b;
       }
       catch(RuntimeException e)
       {
       }
       catch(Exception e2)
       {
       }
       finally
       {
        b += 10;
        return b;
       }
      }
    }
    A. 10
    B. 20 
    C. 30
    D. 40
    解析：
        1. try中有return，先执行finally语句块，在执行return语句。
        2. finally中有return语句，直接执行，返回结果，不再进入try语句块中执行return语句。
        
3. 下面函数将返回？(C)
    A. 1
    B. 2
    C. 3
    D. 编译错误
	解析：
		1. try中有return，先执行finally语句块，在执行return语句。
		2. finally中有return语句，直接执行，返回结果，不再进入try语句块中执行return语句。
	
4. 下列程序的运行结果可能是 （A）
	public void getCustomerInfo() {
        try {
            // do something that may cause an Exception
        } catch (java.io.FileNotFoundException ex) {
            System.out.print("FileNotFoundException!");
        } catch (java.io.IOException ex) {
            System.out.print("IOException!");
        } catch (java.lang.Exception ex) {
            System.out.print("Exception!");
        }
    }
    A. IOException!
    B. IOException!Exception!
    C. FileNotFoundException!IOException!
    D. FileNotFoundException!IOException!Exception!
    解析：这道题问的是可能的结果。
    	注意一点的是：三个catch语句，只会输出其中之一。
```



