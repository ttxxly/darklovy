[比赛链接](http://codeforces.com/contest/828)

## A. Restaurant Tables

time limit per test1 second  
memory limit per test256 megabytes  
inputstandard input  
outputstandard output  

In a small restaurant there are a tables for one person and b tables for two persons.

It it known that n groups of people come today, each consisting of one or two people.

If a group consist of one person, it is seated at a vacant one-seater table. If there are none of them, it is seated at a vacant two-seater table. If there are none of them, it is seated at a two-seater table occupied by single person. If there are still none of them, the restaurant denies service to this group.

If a group consist of two people, it is seated at a vacant two-seater table. If there are none of them, the restaurant denies service to this group.

You are given a chronological order of groups coming. You are to determine the total number of people the restaurant denies service to.

### Input

The first line contains three integers n, a and b (1 ≤ n ≤ 2·105, 1 ≤ a, b ≤ 2·105) — the number of groups coming to the restaurant, the number of one-seater and the number of two-seater tables.

The second line contains a sequence of integers t1, t2, ..., tn (1 ≤ ti ≤ 2) — the description of clients in chronological order. If ti is equal to one, then the i-th group consists of one person, otherwise the i-th group consists of two people.

### Output

Print the total number of people the restaurant denies service to.

### InputSample

```
4 1 2
1 2 1 1
4 1 1
1 1 2 1
```
### OutputSample

```
0
2
```



### Note

In the first example the first group consists of one person, it is seated at a vacant one-seater table. The next group occupies a whole two-seater table. The third group consists of one person, it occupies one place at the remaining two-seater table. The fourth group consists of one person, he is seated at the remaining seat at the two-seater table. Thus, all clients are served.

In the second example the first group consists of one person, it is seated at the vacant one-seater table. The next group consists of one person, it occupies one place at the two-seater table. It's impossible to seat the next group of two people, so the restaurant denies service to them. The fourth group consists of one person, he is seated at the remaining seat at the two-seater table. Thus, the restaurant denies service to 2 clients.

### 题目大意

餐厅有一人座、双人座的桌子， 现在有多个团过来咯， 团队有一个人的， 有两个人的。

如果是一个人：

* 先看有没有空的一人座（a）
* 如果没有一个座，就做空的两人座。（b）
* 如果没有空的一个座和两人座，那么就看有没有两人座有空的.（nb）
* 如果都没有，就不让你进来坐了。（ans++）

如果是两个人：

* 看有没有的空的两人座(b)
* 如果没有，就不让你坐（ans += 2）

我开始没有看清楚题意， 如果没有空的一人座，我就先看的是两人座有没有一个位置是空的（nb），所以错了。

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

int main()
{
    int num, a, b;

    while(cin >> num >> a >> b)
    {
        int nb = 0;
        int c;
        int ans = 0;
        for(int i=0; i<num; i++)
        {
            cin >> c;
            if(c == 1)
            {
                if (a > 0)  a--;
                else if(b > 0)    b--,nb++;
                else if(nb > 0)   nb--;
                else ans++;
            }
            else
            {
                if(b > 0)    b--;
                else    ans += 2;
            }
        }
        printf("%d\n", ans);
    }

    return 0;
}
```