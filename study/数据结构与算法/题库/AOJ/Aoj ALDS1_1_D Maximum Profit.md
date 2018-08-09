链接：[戳我](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_1_D) 

#### Description

You can obtain profits from foreign exchange margin transactions.

你可以从外汇保证金交易中获得利润。

For example, if you buy 1000 dollar at a rate of 100 yen per dollar, and sell them at a rate of 108 yen per dollar, you can obtain (108 - 100) × 1000 = 8000 yen.

例如，如果你以每美元100日元的价格购买1000美元，以108日元/美元的价格卖出，你可以获得(108-100)1000=8000日元。

Write a program which reads values of a currency Rt at a certain time t (t=0,1,2,...n−1), and reports the maximum value of Rj−Ri where j>i 

编写一个程序，它在特定的时间t读取货币Rt的值(t=0,1,2，…n -1)，并报告Rj−Ri的最大值(j>I)。

#### Input

The first line contains an integer n. In the following n lines, Rt (t=0,1,2,...n−1t=0,1,2,...n−1) are given in order.

第一行包含一个整数n。在下列n行中，Rt(t=0,1,2，.n 1)是按顺序排列的。

#### Output

Print the maximum value in a line.

在一行中打印最大的值。

#### Constraints

- 2≤n≤200,000
- 1≤Rt≤10^9

#### Sample Input 

```
6
5
3
1
3
4
3
3
4
3
2
```

#### Sample Output 

```
3
-1
```

#### Analyze

给定一组数据，求它们之间的最大差值。

这里给出一种 O(n) 的算法。

根据题目条件， Rj−Ri where j>i ，以第一组数据为例：

```
5 3 1 3 4 3 这组数据，就有
3 - 5 = -2

1 - 3 = -2
1 - 5 = -4

3 - 1 = 2
3 - 3 = 0
3 - 5 = -2

4 - 3 = 1
4 - 1 = 3
4 - 3 = 1
4 - 5 = -1

3 - 4 = -1
3 - 3 = 0
3 - 1 = 2
3 - 3 = 0
3 - 5 = -2

所以最大差值就是 3， 
对于 A - S = N 这个算式来说，A不变的情况下，S越小，差值N就越大，
所以上述步骤可简化为

3 - 5 = -2

1 - min(3,5) = -2

3 - min(1,3,5) = 2

4 - min(3,1,3,5) = 3

3 - min(4,3,1,3,5) = 2

```

#### Code

```
#include <iostream>
#include <limits.h>
#include <cstdio>
using namespace std;

int r[200010];

int main()
{
    int n;

    while(cin >> n)
    {
        for(int i=0; i<n; i++)
            cin >> r[i];

        int Max = INT_MIN;
        int Min = r[0];
        for(int i=1; i<n; i++)
        {
            Max = max(Max, r[i] - Min);
            Min = min(Min, r[i]);

        }

        cout << Max << endl;
    }


    return 0;
}
```

