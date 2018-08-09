题目链接：[戳我](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1724) 

#### Description

Given a range [a, b], you are to find the summation of all the odd integers in this range.

 给定范围[a,b]，你要找到这个范围内所有奇数的总和。

For example,the summation of all the odd integers in the range [3, 9] is 3 + 5 + 7 + 9 = 24.

例如，在范围[3,9]中，奇数和为：3 + 5 + 7 + 9 = 24.

#### Input

There can be at multiple test cases.

可以有多个测试用例

 The first line of input gives you the number of test cases, T(1 ≤ T ≤ 100).

输入的第一行给出了测试用例的数量，T(1 ≤ T ≤ 100).

 Then T test cases follow. Each test case consists of 2 integers a and b (0 ≤ a ≤ b ≤ 100)
in two separate lines.

然后后面跟着T个测试用例。每个测试用例占两行，包含两个整数a和b(0 ≤ a ≤ b ≤ 100)。

#### Output

For each test case you are to print one line of output – the serial number of the test case followed by the summation of the odd integers in the range [a, b].

对于每个测试用例，您将输出一行：测试用例的序列号后面是[a,b]范围内奇数个整数之和。

#### Sample Input

```
2
1
5
3
5
```

#### Sample Output

```
Case 1: 9
Case 2: 8
```

#### analysis

设在[a,b]范围内奇数有k个, Sn表示[1,n]内奇数个，根据公式：

1 + 3 + 5 + .. (2*k-1) = k(1 + 2*k-1)/2 = k^2

S = Sb - S(a-1) = ((b+1)/2) ^2 - (a/2)^2;

#### code

```
#include <stdio.h>
#include <iostream>
using namespace std;

int main()
{
    int T;
    int a, b;

    scanf("%d", &T);
    for(int i=1; i<=T; i++)
    {
        cin>> a >> b;
        a = a / 2;
        b = (b + 1) / 2;
        printf("Case %d: %lld\n", i, b*b -a*a);

    }
    return 0;
}
```



