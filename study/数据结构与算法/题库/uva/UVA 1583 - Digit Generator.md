## Digit Generator

#### 关键词：模拟

### Description

For a positive integer N , the digit-sum of N is defined as the sum of N itself and its digits. When M is the digitsum of N , we call N a generator of M .
For example, the digit-sum of 245 is 256 (= 245 + 2 + 4 + 5). Therefore, 245 is a generator of 256.
Not surprisingly, some numbers do not have any generators and some numbers have more than one generator. For example, the generators of 216 are 198 and 207.
You are to write a program to find the smallest generator of the given integer.

### Input

Your program is to read from standard input. The input consists of T test cases. The number of test cases T is given in the first line of the input. Each test case takes one line containing an integer N , 1<=N<=100000.

### Output

Your program is to write to standard output. Print exactly one line for each test case. The line is to contain a generator of N for each test case. If N has multiple generators, print the smallest. If N does not have any generators, print 0.
The following shows sample input and output for three test cases.

### SampleInput

```
3 
216 
121 
2005
```

### SampleOutput

```
198 
0 
1979
```
### Hint

### Source

### Analyze

大致题意：如果x加上x的各位数字之和得到y，那么就说x是y的生成元，现在给你一个N，让你求N的最小生成元。

### Code

```
#include <cstdio>  
#include <cstring>  
#include <algorithm>  
#include <iostream>  
using namespace std;  
  
int ans[100009];  
  
int main()  
{  
    int n;  
    int num;  
  
    scanf("%d", &n);  
    memset(ans, 0, sizeof(ans));  
  
    while(n--)  
    {  
        cin>>num;  
        int ans1 = 0,tmp, tmp1;  
  
        if(ans[num])  
            printf("%d\n", ans[num]);  
        else  
        {  
            for(int i=num-45; i<num; i++)//N最大为100000 各个位数字之和最大是9 * 5 = 45  
            {  
                if(i < 0)  
                {  
                    i = 0;  
                    continue;  
                }  
                tmp = i, tmp1=i;  
                while(tmp)  
                {  
                    tmp1 += tmp%10;  
                    tmp /= 10;  
                }  
                if(tmp1 == num)  
                {  
                    ans1 = i;  
                    break;  
                }  
            }  
            ans[num] = ans1;  
            printf("%d\n", ans[num]);  
        }  
  
    }  
  
    return 0;  
}  
```