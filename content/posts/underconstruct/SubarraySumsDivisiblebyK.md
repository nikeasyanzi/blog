```python
class Solution:
    def subarraysDivByK(self, A, K):
        """
        :type A: List[int]
        :type K: int
        :rtype: int
        """
        summ = 0
        res = 0
        dic = {0:1}
        for a in A:

            #print ("a=",a,"sum=",summ);
            summ = (summ + a) % K

            if summ in dic:
                res += dic[summ]
                dic[summ] += 1
            else:
                dic[summ] = 1
            #print("dict=",dic);

        return res
```

這題主要是用prefix sum,

這種我最不熟 

[ZitaoWang](https://leetcode.com/zitaowang)解釋了

```
We initialize the result res = 0. 

We iterate over A, and use a variable summ to keep track of prefix sum up to current index i modulo K,

i.e., summ = (A[0] + ... A[i]) % K. 

If some subarray ending with i has sum divisible by K, 

it means that (A[j] + ... + A[i]) % K == 0 for some j < i, 

which equivalently means that (A[0] + ... + A[j]) % K == summ. 

If we use to dictionary dic to count the number of appearances of all prefix sums modulo K ending with j for all j < i,

then the number of subarrays ending with i that has sum divisible by K is dic[summ], 

so we increment res: res += dic[summ], and increment the count of summ: dic[summ] += 1. 

Finally, we return res.
```

example:

\[4,5,0,-2,-3,1\]   5

a  
= 4 sum= 0

dict= {0: 1, 4: 1}

a= 5 sum= 4

dict= {0: 1, 4: 2}

a= 0 sum= 4

dict= {0: 1, 4: 3}

a= -2 sum= 4

dict= {0: 1, 4: 3, 2: 1}

a= -3 sum= 2

dict= {0: 1, 4: 4, 2: 1}

a= 1 sum= 4

dict= {0: 2, 4: 4, 2: 1}

當 5, 0 都檢查過時,dict 的counter 也加到3

又因為mod 餘數可負

我們會加回k 剛好可以解決有負數的問題

\#Reference:

[https://leetcode.com/problems/subarray-sums-divisible-by-k/discuss/218015/Python-solution](https://leetcode.com/problems/subarray-sums-divisible-by-k/discuss/218015/Python-solution)

