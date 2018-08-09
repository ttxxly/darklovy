[题目链接]( http://acm.hdu.edu.cn/showproblem.php?pid=2035)

## 人见人爱A^B

Time Limit: 2000/1000 MS (Java/Others)  
Memory Limit: 65536/32768 K (Java/Others)  
Total Submission(s): 42396    Accepted Submission(s): 28627

### Description

求A^B的最后三位数表示的整数。
说明：A^B的含义是“A的B次方”

### Input

输入数据包含多个测试实例，每个实例占一行，由两个正整数A和B组成（1<=A,B<=10000），如果A=0, B=0，则表示输入数据的结束，不做处理。

### Output

对于每个测试实例，请输出A^B的最后三位表示的整数，每个输出占一行.

### SampleInput

```
2 3
12 6
6789 10000
0 0
```

### SampleOutput

```
8
984
1
```

### Analyze

求A^B的末尾3位数是多少，其实就是A^B%1000.这个就是快速幂模。

### Code 

```
#include <cstdio>  
#include <algorithm>  
#include <iostream>  
using namespace std;  
#define LL long long  
  
LL mod_pow(LL a, LL b, LL p)  
{  
    LL ans =  1;  
    while(b > 0)    {  
        if(b&1) ans = (ans * a) % p;  
        a = (a * a) % p;  
        b >>= 1;  
    }  
    return ans;  
}  
  
int main()  
{  
    LL a, b;  
  
    while(cin>>a>>b && (a+b))  
    {  
        cout << mod_pow(a, b, 1000) << endl;  
    }  
    return 0;  
}  
```