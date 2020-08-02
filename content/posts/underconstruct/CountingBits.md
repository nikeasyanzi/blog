[7.Bit Manipulation](/bit-manipulation.md)

[338. Counting Bits](https://leetcode.com/problems/counting-bits/description/)


這題有幾件事需要先理解

* 偶數的話，二進為1的位數等於i/2 中1的位數    
    ex. 2(10)和4(100)  4(100)和 8(1000)
* 奇数的話，二進為1的位數等於i-1中1的位數 + 1
    ex. 3(11)和2(10)
所以我們可以用動態規劃來解決這個問題
    
https://leetcode.com/problems/counting-bits/description/
```python
class Solution:
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """

        ans = [0]*(num+1);
        for x in range(1, num+1):
            #print (x);
            ans[x] = ans[x>>1] + (x & 1);
            
        #print (ans);
        return ans;
```

因为 i&(i-1) 的结果是将i的二进制表示中最右边的‘1’消除掉，因此i中1的个数和i&(i-1)中1的个数相差1.

ans[n] = ans[n & (n - 1)] + 1


这个题用DP的方法。把第i个数分成两种情况，如果i是偶数那么，它的二进制1的位数等于i/2中1的位数；如果i是奇数，那么，它的二进制1的位数等于i-1的二进制位数+1，又i-1是偶数，所以奇数i的二进制1的位数等于i/2中二进制1的位数+1. 所以上面的这些可以很简单的表达成answer[i] = answer[i >> 1] + (i & 1)。

answer[i] = answer[i >> 1] + (i & 1)。



i  |  bin   |  '1' |   i&(i-1)
-----------------------
0  |  0000  |  0   |
-----------------------
1    0001    1    0000
-----------------------
2    0010    1    0000
3    0011    2    0010
-----------------------
4    0100    1    0000
5    0101    2    0100
6    0110    2    0100
7    0111    3    0110
-----------------------
8    1000    1    0000
9    1001    2    1000
10   1010    2    1000
11   1011    3    1010
12   1100    2    1000
13   1101    3    1100
14   1110    3    1100
15   1111    4    1110

"""

