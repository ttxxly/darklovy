链接：http://poj.org/problem?id=3278

## Catch That Cow

#### 关键词： BFS

### Description

Farmer John has been informed of the location of a fugitive cow and wants to catch her immediately. He starts at a point N (0 ≤ N ≤ 100,000) on a number line and the cow is at a point K (0 ≤ K ≤ 100,000) on the same number line. Farmer John has two modes of transportation: walking and teleporting.
* Walking: FJ can move from any point X to the points X - 1 or X + 1 in a single minute
* Teleporting: FJ can move from any point X to the point 2 × X in a single minute.
If the cow, unaware of its pursuit, does not move at all, how long does it take for Farmer John to retrieve it?

### Input

Line 1: Two space-separated integers: N and K

### Output

Line 1: The least amount of time, in minutes, it takes for Farmer John to catch the fugitive cow.

### Sample Input
`5 17`

Sample Output

`4`

### Hint

The fastest way for Farmer John to reach the fugitive cow is to move along the following path: 5-10-9-18-17, which takes 4 minutes.

### Source

USACO 2007 Open Silver

### Analyze

题意：从N变到K需要几步，可以N-1,N=1,N*2三种变换方式.
思路：BFS搜索吧；

### CODE

```c++
#include <iostream>
#include <cstring>
#include <queue>
#include <algorithm>
using namespace std;
#define maxn 100009
int n, k;
struct node
{
    int sum, step;
};
bool vis[maxn];
int  bfs()
{
    queue <node> T;
    node st;
    st.step = 0;st.sum = n;
    T.push(st);

    while(!T.empty())
    {
        node tmp = T.front();
        T.pop();
        if(tmp.sum == k)
            return tmp.step;
        if(tmp.sum*2-1  <= maxn && tmp.sum*2>=0 && !vis[tmp.sum*2])
        {
            vis[tmp.sum*2] = true;
            node N = tmp;
            N.step++;N.sum = tmp.sum * 2;
            T.push(N);
        }
        if(tmp.sum-1 <= maxn && tmp.sum-1>=0 && !vis[tmp.sum-1])
        {
            vis[tmp.sum-1] = true;
            node N = tmp;
            N.step++;N.sum = tmp.sum - 1;
            T.push(N);
        }
        if(tmp.sum+1 <= maxn && tmp.sum+1>=0 && !vis[tmp.sum+1])
        {
            vis[tmp.sum+1] = true;
            node N = tmp;
            N.step++,N.sum = tmp.sum+1;
            T.push(N);
        }
    }
}
int main()
{
    while(cin>>n>>k)
    {
        memset(vis, false, sizeof(vis));
       cout <<  bfs() << endl;
    }
    return 0;
}
```




