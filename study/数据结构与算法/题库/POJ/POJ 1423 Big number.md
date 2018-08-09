[题目来源](http://poj.org/problem?id=1423)

### Description

In many applications very large integers numbers are required. Some of these applications are using keys for secure transmission of data, encryption, etc. In this problem you are given a number, you have to determine the number of digits in the factorial of the number.

在许多应用程序中，需要使用非常大的整数。其中一些应用程序正在使用密钥进行数据的安全传输，加密等等。在这个问题中，您得到一个数字，您必须确定数字的阶乘的位数

### Input

输入由几行整数数组成。第一行包含一个整数n，这是要测试的情况的数量，后面是n行，每行一个整数 1 <= m <= 10^7 

### Output

输出包含输入中出现的整数的阶乘的位数。

### Sample Input

```
2
10
20
```

### Sample Output

```
7
19
```

### Source

Dhaka 2002

### Analyze

考的是 Stirling 公式。。。

z = x ^ y => y = logx z   
我们易知 n 的位数为 (lg n) + 1

当 n 很大时， n! 接近于 sqrt(2 * PI * n (n/e)^n ).

两边取对数：

lg n! = (lg 2*PI*n) / 2 + n * lg n/e

所以：

n! 的位数为： res = (lg 2*PI*n) / 2 + n * lg n/e + 1;

### Code

```c++
#include <cstdio>
#include <algorithm>
#include <iostream>
#include <cstring>
#include <fstream>
#include <map>
#include <queue>
#include <set>
#include <cstdlib>
#include <ctime>
#include <vector>
#include <cmath>
#include <limits.h>
using namespace std;

const double e = 2.7182818284590452354, pi = 3.141592653589793239;

double strling_digits_num(int n)
{
	return log10(2*pi*n)/2.0+n*(log10(n/e));     //0ms
	//return log10( sqrt( 2 * pi * n ) ) + n * log10( n / e );    //16ms
}
 
int main()
{
	int t;
	cin>>t;
	while(t--)
	{
		int n;
		cin>>n;
		double m=0;
		m=strling_digits_num(n);
		int answer=(int)m;
		//注意！！！！10的n次方有n+1位数字
		answer++;
		cout<<answer<<endl;
	}
	system("pause");
	return 0;
}
```