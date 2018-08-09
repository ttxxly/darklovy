链接： http://acm.nefu.edu.cn/JudgeOnline/problemShow.php?problem_id=115


## 斐波那契的整除

Problem:115  
Time Limit:1000ms  
Memory Limit:65536K

#### 关键词： 基础题

### Description

已知斐波那契数列有如下递归定义，f(1)=1,f(2)=1, 且n>=3,f(n)=f(n-1)+f(n-2)，它的前几项可以表示为1， 1，2 ，3 ，5 ，8，13，21，34…，现在的问题是想知道f(n)的值是否能被3和4整除，你知道吗？

### Input

输入数据有若干组，每组数据包含一个整数n（1 < n < 1000000000）。

### Output

对应每组数据n，若 f(n)能被3整除，则输出“3”； 若f(n) 能被4整除，则输出“4”；如果能被12整除，输出“YES”；否则输出“NO”。

### SampleInput

```
4
6
7
12
```

### SampleOutput

```
3
4
NO
YES
```

### Hint

### Source

### Analyze

f(n)能被3整除，当且仅当n可以被4整除；f(n)能被4整除，当且仅当n可以被6整除。f(n)能被12整除，当且仅当n可以被12整除(4和6的最小公倍数)

### Code

```
#include <cstdio>  
#include <iostream>  
using namespace std;  
  
int main()  
{  
    long long n;  
  
    while(cin >> n)  
    {  
        if(n % 12 == 0)  
            cout << "YES" << endl;  
        else if(n % 4 == 0)  
            cout << "3"<< endl;  
       else  if(n % 6 == 0)  
            cout << "4" << endl;  
        else  
            cout << "NO" << endl;  
  
    }  
    return 0;  
}
```