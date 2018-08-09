Math中定义了许多的方法，且这些方法均为static类型，通过Math类就能直接调用。

#### 三角函数方法

```
角的三角正弦
	static double  sin(double a )
角的三角余弦
	static  double cos(double a)
角的三角正切
	static  double tan(double  a)
角的反正弦
	static  double asin(double a)
角的反余弦
	static  double acos(double a)
角的反正切
	static  double atan(double a)
角转换为弧度
	static  double toRadians(double a)
弧度转化为角
	static  doueble toDegrees(double a)
```

#### 指数函数方法：

```
获取e的a次方
	static  double exp(double a) 
lna
	static  double log(double a)
log10a
	static  double log10(double a) 
取a的平方根	
	static  double sqrt(double a )
取a的立方根
	static  double cbrt(double a)
求a的b次方
	static  double pow(double a, double b) 
```

#### 取整函数方法

```
求大于等于a的整数值，返回值类型为double
	static double ceil(double a)：
求小于等于a的整数值，返回值类型为double
	static double floor(double a)
求与a最接近的整数值，返回值类型为double如果两个同为整数且同样接近，选取偶数值的那个）
	static double rint(double a) 
```

#### 相关面试题

##### 1. Math.floor(-8.5)=(  )

```
A. (float)-8.0
B. (long)-9
C. (long)-8
D. (double)-9.0
解析：答案：D
    floor:返回小于等于该数的最大整数(返回double类型)；
    ceil:返回大于等于该数的最小整数(返回double类型)；
    round:返回对该数四舍五入的整数(返回int类型)
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79837156