# [3.Array/String](/arraystring.md)


## 3.Longest Substring Without Repeating Characters


[https://leetcode.com/problems/longest-substring-without-repeating-characters/description/](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

    
    Given a string, find the length of the longest substring without repeating characters.
    
    Examples:
    
    Given "abcabcbb", the answer is "abc", which the length is 3.
    
    Given "bbbbb", the answer is "b", with the length of 1.
    
    Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
    

```c
int resetHashTable(int *A)
{
    int i=0;
    for(i=0; i<256; i++)
    {
        A[i]=-1;
    }
    return 0;
}
int lengthOfLongestSubstring(char* s)
{
    int hashTable[256]; //store the index that we visit the char
    int tmp_length=0;
    int max_length=0;

    int left=0; //record the start idx of the sub string
    int j=0;
    resetHashTable(hashTable);

    while(s[j]!='\0')
    {
        if(hashTable[s[j]]!=-1)
        {
            if(hashTable[s[j]]>=left)
            {
                tmp_length=j-left;
                max_length=max_length>tmp_length?max_length:tmp_length;
                left=hashTable[s[j]]+1;
            }
        }
        hashTable[s[j]]=j;
        j++;
    }
    tmp_length=j-left;
    max_length=max_length>tmp_length?max_length:tmp_length; // check the residual string
    return max_length;
}
```
解法:

1. 用set 的方式

    1. 如果某char 出現 便加入set

    [https://www.youtube.com/watch?v=ZlCxw1VUYj0]   (https://www.youtube.com/watch?v=ZlCxw1VUYj0)

    length 就是 目前set 的element 數

2. 用字串計算的方式

    1. 須注意  更新len的問題
if(hashTable[s[j]]>=left)
見 範例pwwkewp, i=6時,
p已拜訪過,但 hashTable[s[j]]=0, left=3

    2. hash array
    
    ASCII 大小是256 所以宣告256 hash array size  
    另外技巧是hash array 用於記錄某字元出現的的idx, so we initialize the array with -1
    3. 迴圈跑完後  再比較一次殘餘的字串有沒有超過目前substring長度

推導  

EX. 
**p w w k e w p**
    
i| 0(p) | 1(w) | 2(w) | 2(w)| 3(k) | 4(e) | 5(w) | 5(w) | 6(p)
:--- |: --- | :---
left=(hashtable[i]+1)| p(0)| p(0)|p(0)| **w(2)**| w(2)| w(2)| w(2)| **k(3)**| k(3)
hashtable| p| p,w(1)|p,w(1)|p,**w(2)**|p,w(2),k|p,w(2),k,e|p,w(2),k,e|p,**w(5)**,k,e|**p(6)**,w(5),k,e
len=i-left|||**len=2**||||**len=5-2=3**|||

EX.
**d v d f**

i| 0(d) | 1(v) | 2(d) | 2(d)| 3(f) | 
:--- |: --- | :---
left=(hashtable[i]+1)| d(0)| d(0)|d(0)| **v(2)**|v(2) 
hashtable| d| d,v(1)|d,v(1)|**d(2)**,v|d(2),v,f
len=i-left|||**len=2**|||

ex.tmmzuxt



