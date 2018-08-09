链接: http://poj.org/problem?id=2034

## Anti-prime Sequences

Time Limit: 3000MS		Memory Limit: 30000K  
Total Submissions: 3803		Accepted: 1726  

#### 关键词： DFS

### Description

Given a sequence of consecutive integers n,n+1,n+2,...,m, an anti-prime sequence is a rearrangement of these integers so that each adjacent pair of integers sums to a composite (non-prime) number. For example, if n = 1 and m = 10, one such anti-prime sequence is 1,3,5,4,2,6,9,7,8,10. This is also the lexicographically first such sequence. 

We can extend the definition by defining a degree danti-prime sequence as one where all consecutive subsequences of length 2,3,...,d sum to a composite number. The sequence above is a degree 2 anti-prime sequence, but not a degree 3, since the subsequence 5, 4, 2 sums to 11. The lexicographically .rst degree 3 anti-prime sequence for these numbers is 1,3,5,4,6,2,10,8,7,9. 

### Input

Input will consist of multiple input sets. Each set will consist of three integers, n, m, and d on a single line. The values of n, m and d will satisfy 1 <= n < m <= 1000, and 2 <= d <= 10. The line 0 0 0 will indicate end of input and should not be processed.

### Output

For each input set, output a single line consisting of a comma-separated list of integers forming a degree danti-prime sequence (do not insert any spaces and do not split the output over multiple lines). In the case where more than one anti-prime sequence exists, print the lexicographically first one (i.e., output the one with the lowest first value; in case of a tie, the lowest second value, etc.). In the case where no anti-prime sequence exists, output 

No anti-prime sequence exists. 

### SampleInput

```
1 10 2
1 10 3
1 10 5
40 60 7
0 0 0
```

### SampleOutput

```
1,3,5,4,2,6,9,7,8,10
1,3,5,4,6,2,10,8,7,9
No anti-prime sequence exists.
40,41,43,42,44,46,45,47,48,50,55,53,52,60,56,49,51,59,58,57,54
```

### Source

East Central North America 2004

### Analyze

有数列 n, n+1, ..., m 还有k， 重新找一个数列，使得这个数列中的k个连续数字的和是合数。

这个就是裸DFS

### Code

```
#include <cstdio>  
#include <cstring>  
#include <iostream>  
#include <algorithm>  
using namespace std;  
  
int n, m, k,sum;  
int ans[1009];  
bool is_prime[10009], vis[1009];  
void init()  
{  
    //因为题目要求是最多有10个小于1000  
    //所以你的素数最好初始化到10009，  
    //不然就会超时，嘿嘿。我在这里错咯几次  
    memset(is_prime, true, sizeof(is_prime));  
    is_prime[0] = is_prime[1] = false;  
    for(int i=2; i<10009; i++)  
        for(int j=2; i*j<10009; j++)  
            is_prime[i*j] = false;  
}  
bool place(int cur, int bak)  
{  
    if(cur == 0)  
        return true;  
    int tmp = cur-k+1;  
    if(tmp < 0)  
        tmp = 0;  
    int sum = bak;  
    for(int i=cur-1; i>=tmp; i--)  
    {  
        sum += ans[i];  
        if(is_prime[sum])  
            return false;  
    }  
    return true;  
}  
void DFS(int cur)  
{  
    if(sum)  
        return;  
    if(cur == m-n+1)  
    {  
        sum ++;  
        for(int i=0; i<m-n+1; i++)  
            printf("%d%c", ans[i], (i==(m-n)?'\n':','));  
        return;  
    }  
    for(int i=n; i<=m; i++)  
    {  
        if(!vis[i] && place(cur, i) )  
        {  
            ans[cur] = i;  
            vis[i] = true;  
            DFS(cur+1);  
            vis[i] = false;  
        }  
    }  
    return;  
}  
int main()  
{  
    init();  
    while(scanf("%d%d%d", &n,&m,&k)!=EOF&&n&&m&&k)  
    {  
        memset(vis, false, sizeof(vis));  
        sum = 0;  
        DFS(0);  
        if(sum == 0)  
            printf("No anti-prime sequence exists.\n");  
    }  
    return 0;  
} 
```
