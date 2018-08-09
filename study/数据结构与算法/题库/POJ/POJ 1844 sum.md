[题目来源](http://poj.org/problem?id=1844)

### Description

有从 1 到 n 个数， 现在通过加号或者是减号将这 n 个数连接起来，这个表达式的值为 S . 现在给你一个 s， 让你求出最小的 n 是多少？ 


### Input

输入S (0< S <= 100000) 

### Output

最小的 n

### Sample Input

```
12
```

### Sample Output

```
7
```

### Hint

The sum 12 can be obtained from at least 7 terms in the following way: 12 = -1+2+3+4+5+6-7.

### Source

Romania OI 2002

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

#define MAXN 200000

int dp[2][MAXN + 1];

int main()
{
    int n ,i ,j;
    while(cin>>n)
    {
        memset(dp[1], 0, sizeof(dp[1]));	//首先初始第一层结果集
        dp[1][MAXN/2 + 1] = 1;
        dp[1][MAXN/2 - 1] = 1;
        n += MAXN/2;
        for(i=2 ; ; i++)
        {
            memset(dp[i&1], 0, sizeof(dp[i&1]));	//初始当前结果集
            for(j = 0; j <= MAXN; j++)
            {
                if(dp[(i-1)&1][j]) 		//在上一层结果集找
                {
                    if(j + i <= MAXN)   dp[i&1][j + i] = 1;	//在范围内则记录
                    if(j - i >= 0)  dp[i&1][j - i] = 1;
                }
            }
            if(dp[i&1][n]) 		//找到n了就退出循环
            {
                cout<<i<<endl;
                break;
            }
        }
    }
    return 0;
}

```
