# [3. Array/String](/arraystring.md)


##868. Binary Gap
https://leetcode.com/problems/binary-gap/description/


明明很簡單的一題 卻解很久

主要就看是不是1就好 

最後回傳maxLen+1  因為 11 的狀況 maxLen=1;

```c

int binaryGap(int N) {
    int maxLen = -1, curLen = -1;
    
    for(;N != 0;N = N >> 1)
    {
        if(N % 2 == 1)
        {
            maxLen = maxLen > curLen ? maxLen : curLen;
            curLen = 0;
        }
        else
        {
           if(curLen != -1)
           {
               curLen++;
           }
        }
    }
    return maxLen + 1;
}
```