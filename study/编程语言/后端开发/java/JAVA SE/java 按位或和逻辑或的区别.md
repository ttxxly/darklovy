本文主要带领大家了解`|`和`||`的区别

```
|: 按位或
	格式：条件1 | 条件2
	说明：不管条件1是否满足都会执行条件2
||：逻辑或
	格式“条件1 || 条件2
	说明：如果条件1满足就不会执行条件2
```

#### 相关案例

```
1. Given the following code:
    public class Test {
        private static int j = 0;

        private static Boolean methodB(int k) {
            j += k;
            return true;
        }

        public static void methodA(int i) {
            boolean b;
            b = i < 10 | methodB(4);
            b = i < 10 || methodB(8);

        }

        public static void main(String args[]) {
            methodA(0);
            System.out.println(j);
        }
    }
    What is the result? ( B )
        A. The program prints”0”
        B. The program prints”4”
        C. The program prints”8”
        D. The program prints”12”
        E. The code does not complete.
        解析：
        	//i=0, i<10为true，但是依然执行methodB(4),之后 j=4
        	b = i < 10 | methodB(4); 
        	//i=0, i<10位true，可以决定结果，所以不会执行methodB(8)，j依然=4
        	b = i < 10 || methodB(8);
```

