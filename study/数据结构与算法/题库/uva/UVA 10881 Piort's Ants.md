[题目来源](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1822)

### Description

一根长度为 L 厘米的木棍上有 n 只蚂蚁， 每只蚂蚁要么朝左爬， 要么朝右爬， 速度为 1 厘米/秒。 当两只蚂蚁相撞时， 二者同时掉头（掉头时间不计）。 给出每只蚂蚁的初始位置和朝向， 计算 T 秒后每只蚂蚁的位置。

### Input

输入的第一行为数据组数。 每组数据的第一行为 3 个正整数 L, T, n (0 <= n <= 10 000) 以下的 n 行描述一致蚂蚁的初始位置， 其中整数 x 为蚂蚁距离木棍左端的距离， 字母表示初始朝向（L 表示朝左， R 表示朝右）。

### Output

对于每组数据， 输出 n 行， 按照输入顺序输出每只蚂蚁的位置和朝向（Runing 表示正在碰撞）。 在第 T秒之前已经掉下木棍的蚂蚁（正好爬到木棍边缘的不算）输出 Fell off

### SampleInput

```
2
10 1 4 
1 R 
5 R
3 L
10 R
10 2 3
4 R
5 L
8 R
```

### SampleOutput

```
Case #1:
2 Turning
6 R
2 Turning
Fell off
Case #2:
3 L
6 R
10 R
```

### Analyze

1. 计算 T 秒后在哪些位置上有蚂蚁。

单纯从位置来说， 掉头其实等同于对穿而过。 
比如 (1, R) 经过 3 秒后 (4, R)这里一定会有一只蚂蚁（画个图就明白了）。 在这个期间如果发生碰撞， 那么该位置上就不是原来的那只蚂蚁了， 所以我们需要找到 对应关系。

2. 处理每只蚂蚁和位置的对应关系。

画一张图，我们就能明白，其实所有的蚂蚁的相对顺序是没有变的， 我们只需要将目标位置从小到大排序，则从左到右的每个位置分别对应初始状态下从左到右的每只蚂蚁。 

最后还有一个问题是： 题目中给出的数据不一定是按照从左到右的顺序输入， 所以我们还需要预处理计算出输入中的第 i 只蚂蚁的序号 order[i].

### Code

```
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

const int maxn = 10000 + 10;

struct Ant{
    int id; //输入顺序
    int p;  //位置
    int d;  //朝向 -1,左 0 转身中， 1 右
    bool operator < (const Ant& a) const{
        return p <a.p;
    }
}before[maxn], after[maxn];

const char dirName[][10] = {"L", "Turning", "R"};

int order[maxn];    //输入的第 i 只蚂蚁是终态中的左数第 order[i] 只蚂蚁。

int main()
{
    int k;

    scanf("%d", &k);
    for(int kase=1; kase<=k; kase++)
    {
        int L, T, n;
        printf("Case #%d:\n", kase);
        scanf("%d%d%d", &L, &T, &n);
        for(int i=0; i<n; i++)
        {
            int p, d;
            char c;
            scanf("%d %c", &p, &c);
            d = (c == 'L') ? -1 : 1;
            before[i] = (Ant){i, p, d};
            after[i] = (Ant){0, p+T*d, d};
        }

        //计算 order 数组
        sort(before, before+n);
        for(int i=0; i<n; i++) order[before[i].id] = i;

        //计算终态
        sort(after, after+n);
        for(int i=0; i<n-1; i++)
        {
            if(after[i].p == after[i+1].p)
                after[i].d = after[i+1].d = 0;
        }

        //输出结果
        for(int i=0; i<n; i++)
        {
            int a = order[i];
            if(after[a].p < 0 || after[a].p > L)    printf("Fell off\n");
            else    printf("%d %s\n", after[a].p, dirName[after[a].d+1]);
        }
        printf("\n");
    }

    return 0;
}
```
