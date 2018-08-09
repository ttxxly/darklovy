### Description

把手放在键盘上，稍不注意就会往右错一位，这样输入Q会变成W，输入J会变成K.
输入一个错位后敲出的字符串(所有都是大写字母),输出打字员本来想要打出的句子。数据合法.

#### 关键词： 基础题

### Analyze

使用常量数组，查询字符。

### Code

```
#include <cstdio>  
#include <cstring>  
using namespace std;  
  
char str[] = "1234567890-=QWERTYUIOP[]\\ASDFGHJKL;'ZXCVBNM,./";//\\表示“\”  
int main()  
{  
    int c;  
  
    while( (c=getchar()) != EOF)  
    {  
        int i;  
        for(i=1; str[i]!=c&&str[i]; i++);//找错位之后的字符在常量表中的位置  
        if(str[i])//找到就输出他的前一个字符  
            putchar(str[i-1]);  
        else  
            putchar(c);  
    }  
  
    return 0;  
}  
```