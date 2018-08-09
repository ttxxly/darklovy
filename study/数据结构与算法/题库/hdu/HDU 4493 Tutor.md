链接: http://acm.hdu.edu.cn/showproblem.php?pid=4493

[中文翻译](http://www.cnblogs.com/ttxxly/p/6915754.html)

## Tutor

Time Limit: 2000/1000 MS (Java/Others)      
Memory Limit: 65535/65535 K (Java/Others)  
Total Submission(s): 4265    Accepted Submission(s): 1118

#### 关键词：模拟

### Description

Lilin was a student of Tonghua Normal University. She is studying at University of Chicago now. Besides studying, she worked as a tutor teaching Chinese to Americans. So, she can earn some money per month. At the end of the year, Lilin wants to know his average monthly money to decide whether continue or not. But she is not good at calculation, so she ask for your help. Please write a program to help Lilin to calculate the average money her earned per month.

### Input

The first line contain one integer T, means the total number of cases. 
Every case will be twelve lines. Each line will contain the money she earned per month. Each number will be positive and displayed to the penny. No dollar sign will be included.

### Output

The output will be a single number, the average of money she earned for the twelve months. It will be rounded to the nearest penny, preceded immediately by a dollar sign without tail zero. There will be no other spaces or characters in the output.

### SampleInput

```
2 
100.00 
489.12 
12454.12 
1234.10 
823.05 
109.20 
5.27 
1542.25 
839.18 
83.99 
1295.01 
1.75
100.00 
100.00 
100.00 
100.00 
100.00 
100.00 
100.00 
100.00 
100.00 
100.00 
100.00 
100.00

```

### SampleOutput

```
$1581.42 
$100
```

### Hint

### Source

2013 ACM-ICPC吉林通化全国邀请赛——题目重现

### Analyze

大致题意：给出12个浮点正数，要求这12个数的平均值。（忽略无效0）.比如1.90，就要输出1.9. 注意一点就是：结果要求四舍五入到最接近的美分。坑点在这里。。。。

100美分 = 1美元， 换句话说就是保留两位小数了。。。

大致思路：运用sprintf()函数将平均值sum,保留两位小数输入到一个字符串中，进行处理。

### Code

```c++
#include <cstdio>
#include <algorithm>
#include <iostream>
#include <cstring>
#include <fstream>
#include <map>
#include <vector>
#include <cmath>
#include <limits.h>
using namespace std;

char ans[1000];

int main()
{
    int n;

    cin >> n;

    while(n--)
    {
        double sum = 0;
        double num = 0;
        for(int i=0; i<12; i++)
        {
            cin >> num;
            sum += num;
        }
        sum /= 12.0;
        sprintf(ans, "%.2f", sum);
        for(int i=strlen(ans)-1; i>=0; i--)
        {
            if(ans[i] == '.')
            {
                ans[i] = '\0';
                break;
            }
            if(ans[i] != '0' )
            {
                ans[i+1] = '\0';
                break;
            }
        }

        printf("$");
        puts(ans);
    }



    return 0;
}

```