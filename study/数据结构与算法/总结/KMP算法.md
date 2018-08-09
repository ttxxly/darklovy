KMP算法是一种改进的字符串匹配算法，由D.E.Knuth，J.H.Morris和V.R.Pratt同时发现，因此人们称它为克努特——莫里斯——普拉特操作（简称KMP算法）。

KMP算法的关键是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。

具体实现就是实现一个next()函数，函数本身包含了模式串的局部匹配信息。时间复杂度O(m+n)。

#### 提出问题

有一个文本串S，和一个模式串P，查找P在S中的位置。

```
思路：
	1. 暴力匹配
		for循环遍历所有的可能。
	2. KMP算法
		实际上就是对暴力匹配的优化，尽量减少匹配次数。
```

暴力代码：

```
int ViolentMatch(char* s, char* p)  
{  
    int sLen = strlen(s);  
    int pLen = strlen(p);  
  
    int i = 0;  
    int j = 0;  
    while (i < sLen && j < pLen)  
    {  
        if (s[i] == p[j])  
        {  
            //①如果当前字符匹配成功（即S[i] == P[j]），则i++，j++      
            i++;  
            j++;  
        }  
        else  
        {  
            //②如果失配（即S[i]! = P[j]），令i = i - (j - 1)，j = 0      
            i = i - j + 1;  
            j = 0;  
        }  
    }  
    //匹配成功，返回模式串p在文本串s中的位置，否则返回-1  
    if (j == pLen)  
        return i - j;  
    else  
        return -1;  
}  
```

#### 怎么减少匹配次数？

看上面的暴力代码，减少匹配次数的关键在于怎样快速找到下一个匹配点.

#### next数组

实际上就是寻找前缀后缀最长公共元素长度。

```
//优化过后的next 数组求法  
void GetNextval(char* p, int next[])  
{  
    int pLen = strlen(p);  
    next[0] = -1;  
    int k = -1;  
    int j = 0;  
    while (j < pLen - 1)  
    {  
        //p[k]表示前缀，p[j]表示后缀    
        if (k == -1 || p[j] == p[k])  
        {  
            ++j;  
            ++k;  
            //较之前next数组求法，改动在下面4行  
            if (p[j] != p[k])  
                next[j] = k;   //之前只有这一行  
            else  
                //因为不能出现p[j] = p[ next[j ]]，所以当出现时需要继续递归，k = next[k] = next[next[k]]  
                next[j] = next[k];  
        }  
        else  
        {  
            k = next[k];  
        }  
    }  
}
```

next数组解决的问题：

```
1. i 不再回溯
2. j 不一定从0开始匹配。
```

完整代码：

```
#include <iostream>
#include <sstream>
#include <iomanip>
#include <vector>
#include <deque>
#include <list>
#include <set>
#include <map>
#include <stack>
#include <queue>
#include <bitset>
#include <string>
#include <numeric>
#include <algorithm>
#include <functional>
#include <iterator>
#include <cstdio>
#include <cstring>
#include <cmath>
#include <cstdlib>
#include <cctype>
#include <complex>
#include <ctime>

using namespace std;

const int MAXN = 100005;

char s[MAXN],p[MAXN];

int next[MAXN];
//优化过后的next 数组求法
void getnext(char* p, int next[])
{
    int pLen = strlen(p);
    next[0] = -1;
    int k = -1;
    int j = 0;
    while (j < pLen - 1)
    {
        //p[k]表示前缀，p[j]表示后缀
        if (k == -1 || p[j] == p[k])
        {
            ++j;
            ++k;
            //较之前next数组求法，改动在下面4行
            if (p[j] != p[k])
                next[j] = k;   //之前只有这一行
            else
                //因为不能出现p[j] = p[ next[j ]]，所以当出现时需要继续递归，k = next[k] = next[next[k]]
                next[j] = next[k];
        }
        else
        {
            k = next[k];
        }
    }
}

int kmp(char *s,char *p)
{
    int lens = strlen(s);
    int lenp = strlen(p);
    int i = 0,j = 0;
    while(i < lens && j < lenp)
    {
        if(j == -1 || s[i] == p[j])
        {
            i++;
            j++;
        }
        else
            j = next[j];
    }
    if(j == lenp)
        return i - j;
    else
        return -1;
}

int main()
{
    //freopen("int.txt","r",stdin);
    //freopen("out.txt","w",stdout);
    cin.getline(s, MAXN);
    cin.getline(p, MAXN);
    getnext(p, next);
    for (int i=0; i<strlen(p); i++)
    {
        printf("%d ", next[i]);
    }
    printf("\n");
    printf("%d\n",kmp(s,p));
    return 0;
}

```

发表于：

```
https://blog.csdn.net/jdliyao/article/details/80030210
微信公众号 - 唯有百炼
```

