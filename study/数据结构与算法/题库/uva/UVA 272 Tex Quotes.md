### Description

在Tex中，左引号是"``",右引号是"''"，输入一篇包含双引号的文章，你的任务是将它转换成Tex格式.

### Code

```
#include <cstdio>  
using namespace std;  
  
  
int main()  
{  
    int c, q = 1;  
  
    while( (c = getchar()) != EOF)  
    {  
        if(c == '"')  
        {  
            printf("%s", q==1?"``":"''");  
            q = -q;  
        }  
        else  
            printf("%c", c);  
    }  
  
    return 0;  
}  
```