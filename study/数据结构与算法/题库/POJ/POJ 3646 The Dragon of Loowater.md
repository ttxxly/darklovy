链接： http://poj.org/problem?id=3646

[中文翻译](http://blog.ttxxly.top/2017/05/31/The-Dragon-of-Loowater/)

## The Dragon of Loowater

### Description

你的王国里有一条 n 个头的恶龙， 你希望雇一些骑士把它杀死（即砍掉所有的头）。

村里有 m 个骑士可以雇佣。 一个能力值为 x 的骑士可以砍掉恶龙一个直径不超过 x 的头， 并且需要支付 x 个金币。 

问： 如何雇佣骑士才能砍掉恶龙的所有头，并花最少的钱？

注意： 一个骑士只能砍掉一个头，且不能被雇佣两次。


### Input

输入包含多组数据。 

每组数据的第一行为正整数 n 和 m （1 <= n,m <= 20 000）。

以下的 n 行， 每行为一个整数， 即恶龙每个头的直径

以下的 m 行为一个整数， 即每个骑士的能力。

输入结束标志为： n == m == 0.


### Output

对于每组数据，输出最少花费。 如果无解， 输出：
 
Loowater is doomed!

### SampleInput

```
2 3
5
4
7
8
4
2 1
5
5
10
0 0
```

### SampleOutput

```
11
Loowater is doomed!
```

### 大致题意

n条恶龙，m个勇士，用勇士来杀恶龙。一个勇士只能杀一个恶龙。而且勇士只能杀直径不超过自己能力值的恶龙。每个勇士需要支付能力值一样的金币。
 
问杀掉所有恶龙需要的最少金币。

### Analyze

将骑士按照能力从小到大排序，在将恶龙的所有头按照直径大小从小到大排序。
然后一个一个砍就完了。


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

const int maxn = 20000 + 5;
int A[maxn], B[maxn];

int main()
{
    int n, m;

    while(scanf("%d%d", &n, &m)==2 && n && m)
    {
        for(int i=0; i<n; i++)  scanf("%d", &A[i]);//恶龙的头
        for(int i=0; i<m; i++)  scanf("%d", &B[i]);//骑士的能力值
        sort(A, A+n);
        sort(B, B+m);
        int cur = 0;    //当前需要砍掉恶龙的头编号,从零开始
        int cost = 0;   //当前总费用

        for(int i=0; i<m; i++)
        {
            if(B[i] >= A[cur])  //表示骑士用能力干掉
            {
                cost += B[i];
                cur++;
            }
            if(cur == n) //所有的头已经砍掉了
                break;
        }
        if(cur < n) printf("Loowater is doomed!\n");
        else        printf("%d\n", cost);
    }

    return 0;
}


```