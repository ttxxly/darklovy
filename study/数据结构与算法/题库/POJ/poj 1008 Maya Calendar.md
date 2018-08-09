
[题目来源](http://poj.org/problem?id=1008)

## Maya Calendar
Time Limit: 1000MS  
Memory Limit: 10000K  
Total Submissions: 78322  
Accepted: 24074

### Description

During his last sabbatical, professor M. A. Ya made a surprising discovery about the old Maya calendar. From an old knotted message, professor discovered that the Maya civilization used a 365 day long year, called Haab, which had 19 months. Each of the first 18 months was 20 days long, and the names of the months were pop, no, zip, zotz, tzec, xul, yoxkin, mol, chen, yax, zac, ceh, mac, kankin, muan, pax, koyab, cumhu. Instead of having names, the days of the months were denoted by numbers starting from 0 to 19. The last month of Haab was called uayet and had 5 days denoted by numbers 0, 1, 2, 3, 4. The Maya believed that this month was unlucky, the court of justice was not in session, the trade stopped, people did not even sweep the floor. 

For religious purposes, the Maya used another calendar in which the year was called Tzolkin (holly year). The year was divided into thirteen periods, each 20 days long. Each day was denoted by a pair consisting of a number and the name of the day. They used 20 names: imix, ik, akbal, kan, chicchan, cimi, manik, lamat, muluk, ok, chuen, eb, ben, ix, mem, cib, caban, eznab, canac, ahau and 13 numbers; both in cycles. 

Notice that each day has an unambiguous description. For example, at the beginning of the year the days were described as follows: 

1 imix, 2 ik, 3 akbal, 4 kan, 5 chicchan, 6 cimi, 7 manik, 8 lamat, 9 muluk, 10 ok, 11 chuen, 12 eb, 13 ben, 1 ix, 2 mem, 3 cib, 4 caban, 5 eznab, 6 canac, 7 ahau, and again in the next period 8 imix, 9 ik, 10 akbal . . . 

Years (both Haab and Tzolkin) were denoted by numbers 0, 1, : : : , where the number 0 was the beginning of the world. Thus, the first day was: 

Haab: 0. pop 0 

Tzolkin: 1 imix 0 
Help professor M. A. Ya and write a program for him to convert the dates from the Haab calendar to the Tzolkin calendar. 

### Input

The date in Haab is given in the following format: 
NumberOfTheDay. Month Year 

The first line of the input file contains the number of the input dates in the file. The next n lines contain n dates in the Haab calendar format, each in separate line. The year is smaller then 5000. 

### Output

The date in Tzolkin should be in the following format: 
Number NameOfTheDay Year 

The first line of the output file contains the number of the output dates. In the next n lines, there are dates in the Tzolkin calendar format, in the order corresponding to the input dates. 

### Sample Input

```
3
10. zac 0
0. pop 0
10. zac 1995
```

### Sample Output

```
3
3 chuen 0
1 imix 0
9 cimi 2801
```

### Source

Central Europe 1995

### Analyze

给出两个日历，第一个日历，一共19个月份，前18个月份，一个月20天，最后一个月5天，一年365天，第二个日历，由20个名称和13个数字组成，构成一年260天，让由第一个日历的时间，得出第二个日历的时间。

map映射，把每个月份都映射成字符串，然后根据第一个日期计算这是第几天。

### Code


```
#include <stdio.h>
#include <string>
#include <string.h>
#include <map>
#include <iostream>
using namespace std;
map <string,int> m;
map <int,string> aidm;
int main()
{
	int T;
	char day[10],month[10];
	int year;
	int sumday;
	int i,j;
	m["pop"]=0;
	m["no"]=1;
	m["zip"]=2;
	m["zotz"]=3;
	m["tzec"]=4;
	m["xul"]=5;
	m["yoxkin"]=6;
	m["mol"]=7;
	m["chen"]=8;
	m["yax"]=9;
	m["zac"]=10;
	m["ceh"]=11;
	m["mac"]=12;
	m["kankin"]=13;
	m["muan"]=14;
	m["pax"]=15;
	m["koyab"]=16;
	m["cumhu"]=17;
	m["uayet"]=18;
	aidm[0]="imix";
	aidm[1]="ik";
	aidm[2]="akbal";
	aidm[3]="kan";
	aidm[4]="chicchan";
	aidm[5]="cimi";
	aidm[6]="manik";
	aidm[7]="lamat";
	aidm[8]="muluk";
	aidm[9]="ok";
	aidm[10]="chuen";
	aidm[11]="eb";
	aidm[12]="ben";
	aidm[13]="ix";
	aidm[14]="mem";
	aidm[15]="cib";
	aidm[16]="caban";
	aidm[17]="eznab";
	aidm[18]="canac";
	aidm[19]="ahau";	
	scanf("%d",&T);
	printf("%d\n",T);
	while(T--){
		sumday=0;
		scanf("%s %s %d",day,month,&year);

		int numday=0;
		for(i=0;day[i]!='.';i++)
			numday=numday*10+day[i]-'0';
		
		sumday = numday + m[month]*20 + year*365;
		int aidyear = sumday/260;
		sumday%=260;
		int temp = sumday%20;
		string aidmonth=aidm[temp];
		int aidday = sumday%13;
		cout<<aidday+1<<" "<<aidmonth<<" "<<aidyear<<endl;
	}
	
	return 0;
}
```
