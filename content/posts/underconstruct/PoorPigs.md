
# [2. Math](/math.md)

## 458. Poor Pigs

    There are 1000 buckets, one and only one of them contains poison, the rest are filled with water. They all look the same. If a pig drinks that poison it will die within 15 minutes. What is the minimum amount of pigs you need to figure out which bucket contains the poison within one hour.

    Answer this question, and write an algorithm for the follow-up general case.

    Follow-up:

    If there are n buckets and a pig drinking poison will die within m minutes, how many pigs (x) you need to figure out the "poison" bucket within p minutes? There is exact one bucket with poison.


```c
#include <math.h>

    int poorPigs(int buckets, int minutesToDie, int minutesToTest) {
    int i=minutesToTest/minutesToDie +1;
    int pigs=1;
    
    if (buckets==1) return 0;
    while( pow(i,pigs) <buckets){
        pigs++;
    }
    return pigs;
}
```


http://www.cnblogs.com/grandyang/p/7664088.html
https://www.jianshu.com/p/789d57102d50