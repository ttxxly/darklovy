链接： http://acm.nyist.edu.cn/JudgeOnline/problem.php?pid=737

## 石子合并（一）

时间限制：1000 ms  |  内存限制：65535 KB  
难度：3  

#### 关键词： 区间DP

### Description

有N堆石子排成一排，每堆石子有一定的数量。现要将N堆石子并成为一堆。合并的过程只能每次将相邻的两堆石子堆成一堆，每次合并花费的代价为这两堆石子的和，经过N-1次合并后成为一堆。求出总的代价最小值。

### Input

有多组测试数据，输入到文件结束。
每组测试数据第一行有一个整数n，表示有n堆石子。
接下来的一行有n（0< n < 200）个数，分别表示这n堆石子的数目，用空格隔开


### Output

输出总代价的最小值，占单独的一行


### SampleInput

```
3
1 2 3
7
13 7 8 16 21 4 18
```

### SampleOuput 

```
9
239
```

### Analyze

1. 第一种实现方式：DP模板：

dp[i][j]： 表示从 第i堆 到 第j堆 总的最小代价。

`dp[i][j] = min(dp[i][j], dp[i][k] + dp[k+1][j] + sum[j] - sum[i-1]);`

2. 优化：平行四边形优化

    以后添加。。。。
    
### Code1

```c++
#include <cstdio>  
#include <climits>  
#include <cstring>  
#include <algorithm>  
using namespace std;  
   
#define N 210  
   
int dp[N][N],sum[N];  
int main()  
{  
   int n;  
   while(~scanf("%d",&n))  
    {  
       int a[N];  
       sum[0]=0;  
       for(int i=1; i<=n; i++)  
       {  
           scanf("%d",&a[i]);  
           sum[i]=sum[i-1]+a[i];  
       }  
       memset(dp,0,sizeof(dp));  
       int i,j,l,k;  
       for(l = 2; l <= n; ++l)  
       {  
           for(i = 1; i <= n - l + 1; ++i)  
           {  
                j = i + l - 1;  
                dp[i][j] = INT_MAX;  
                for(k = i; k < j; ++k)  
                {  
                    dp[i][j] =min(dp[i][j],dp[i][k] + dp[k + 1][j] + sum[j] - sum[i-1]);  
                }  
           }  
       }  
       printf("%d\n", dp[1][n]);  
    }  
   return 0;  
}
```