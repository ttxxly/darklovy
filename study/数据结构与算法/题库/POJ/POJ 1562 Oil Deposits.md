链接： http://poj.org/problem?id=1562

## Oil Deposits

#### 关键词：DFS

### Description

The GeoSurvComp geologic survey company is responsible for detecting underground oil deposits. GeoSurvComp works with one large rectangular region of land at a time, and creates a grid that divides the land into numerous square plots. It then analyzes each plot separately, using sensing equipment to determine whether or not the plot contains oil. A plot containing oil is called a pocket. If two pockets are adjacent, then they are part of the same oil deposit. Oil deposits can be quite large and may contain numerous pockets. Your job is to determine how many different oil deposits are contained in a grid.

### Input

The input contains one or more grids. Each grid begins with a line containing m and n, the number of rows and columns in the grid, separated by a single space. If m = 0 it signals the end of the input; otherwise 1 <= m <= 100 and 1 <= n <= 100. Following this are m lines of n characters each (not counting the end-of-line characters). Each character corresponds to one plot, and is either `*', representing the absence of oil, or `@', representing an oil pocket. 


### Output

are adjacent horizontally, vertically, or diagonally. An oil deposit will not contain more than 100 pockets.

### SampleInput

```
1 1
*
3 5
*@*@*
**@**
*@*@*
1 8
@@****@*
5 5 
****@
*@@*@
*@**@
@@@*@
@@**@
0 0
```

### SampleOutput

```
0
1
2
2
```

### Hint

### Source

Mid-Central USA 1997

### Analyze

大致题意： 给一个矩阵，*代表空地，@代表油田，并且@如果水平，竖直，对角线相邻的话就认为是一块油田，问有多少块油田。

思路: DFS，从第一个字符开始搜，找到一个@就标记一下，cnt++，然后看它的八个方向上是不是有@，如果有，全部标记为*，不需要恢复现场。然后输出cnt的值就行了。

### Code

```
>#include <cstdio>  
#include <cstring>  
#include <algorithm>  
using namespace std;  
  
int m, n, cnt;  
char s[109][109];  
bool flag;  
int dir[8][2] = {{0,1},{0,-1},{-1,0},{1,0},{1,1},{-1,1},{1,-1},{-1,-1}};  
void dfs(int i, int j)  
{  
    if (s[i][j] == '*') return;  
    if(s[i][j] == '@')  
    {  
         s[i][j] = '*';  
         flag = true;  
    }  
    for (int k = 0; k < 8; ++k)  
    {  
        int x = i+dir[k][0];  
        int y = j+dir[k][1];  
        if (s[x][y] == '@' && i >= 0 && j >= 0 && i < m && j < n)  
        {  
            dfs(x, y);  
        }  
    }  
}  
int main(void)  
{  
    while (~scanf("%d%d", &m, &n))  
    {  
        getchar();  
        if(m==0 && n==0)  
            break;  
        cnt = 0;  
        for (int i = 0; i < m; ++i)  
            scanf("%s", s[i]);  
        for (int i = 0; i < m; ++i)  
        {  
            for (int j = 0; j < n; ++j)  
            {  
                if(s[i][j] == '@')  
                {  
                    flag = false;  
                    dfs(i, j);  
                    if (flag)  
                    {  
                        cnt ++;  
//                        printf("ferfergrege\n");  
//                        printf("cnt = %d\n", cnt);  
                    }  
//                    for (int x = 0; x < m; ++x)  
//                        for (int y = 0; y < n; ++y)  
//                            printf("%c%c", s[x][y], (y==n-1)?'\n':' ');  
                }  
            }  
        }  
        printf("%d\n", cnt);  
    }  
  
    return 0;  
} 
```