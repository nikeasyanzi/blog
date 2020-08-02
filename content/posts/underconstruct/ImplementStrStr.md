# [3. Array/String](/arraystring.md)

[28. Implement strStr()](https://leetcode.com/problems/implement-strstr/)

```python
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if needle=="":
            return 0;
        if haystack=="":
            return -1;

        
        lps=self.computLPS(needle);
        
        #print("lps=",lps);
        
        haystack_idx=0;
        needle_idx=0;
        
        while(haystack_idx<len(haystack)):
            if(haystack[haystack_idx]==needle[needle_idx]):
                haystack_idx=haystack_idx+1;
                needle_idx=needle_idx+1;
            if (needle_idx==len(needle)):
                #print("we find match at", haystack_idx-len(needle))
                return haystack_idx-needle_idx;
            
            if(haystack_idx<len(haystack) and haystack[haystack_idx]!=needle[needle_idx]): 
                if(needle_idx!=0):
                    needle_idx=lps[needle_idx-1];
                else:
                    haystack_idx=haystack_idx+1;
        return -1;
    def computLPS(self,pattern):
        lps=[0];
        length=0;
        i=1;
        while(i<len(pattern)):
            if(pattern[i]==pattern[length]):
                length=length+1;
                lps.append(length);
                i=i+1;
            
            else:
                if length!=0:
                    length=lps[length-1];
                else:
                    lps.append(0);

                    i=i+1;
        return lps;
```    

Test case:
"aaa"
"aaaa"

"mississippi"
"issip"


這題就是用KMP (Knuth Morris Pratt) Pattern Searching 演算法

詳情可參考 
https://hackmd.io/YG4jW40RR0qCiqduTajRaw

基本上是要先建立lps lookup table
再去做kmp search

