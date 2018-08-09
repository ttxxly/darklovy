[题目来源](https://icpcarchive.ecs.baylor.edu/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1709)


### Description

在一个周长为 10000 的圆上等距分布着 n 个雕塑。 现在又有 m 个新雕塑加入（位子可以随意放）， 希望所有 n+m 个雕塑在圆周上均匀的分布。 这就需要移动其中一些原来的雕塑。 要求 n 个雕塑移动的总距离尽量小。

### Input

输入包含若干组数据。 每组数据仅一行， 包含两个数据 n 和 m (2 <= n <= 1000, 1 <= m <= 1000), 即原始的雕塑数量和新加的雕塑数量。 输入结束标志为文件结束符。

### Ouput

输出仅一行， 为最小总距离， 精确到 10^(-4).

### SampleInput

```
2 1
2 3
3 1
10 10
```

### SampleOutput

```
1666.6667
1000.0
1666.6667
0.0
```

### Analyze

以后待补， 不知道怎么讲。 没有严格证明, 看书也没有看懂。

### Code

```C++
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

int main()
{
    int n,m;
    while(~scanf("%d%d",&n,&m))
    {
        int i;
        double t,ans = 0;
        for(i = 1;i<=n;i++)
        {
            t = (double)i/n*(n+m);//计算需要移动的雕塑的坐标
            ans+=fabs(t-floor(t+0.5))/(n+m);//累计移动距离
        }
        printf("%.4lf\n",ans*10000);
    }

    return 0;
}

```