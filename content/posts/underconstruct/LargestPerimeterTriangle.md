### 976.Largest Perimeter Triangle

```python
class Solution:
    def largestPerimeter(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        sortedA=sorted(A,reverse=True);
        #print(sortedA);
        """
        for i in range(len(sortedA)):
            if i + 2 < len(sortedA) and sortedA[i + 1] + sortedA[i + 2] > sortedA[i]:
                return sum(sortedA[i:i + 3])

        """

        for i in range(0,len(sortedA)):
            for j in range(i+1,len(sortedA)):
                for k in range(j+1,len(sortedA)):
                    if i + 2 < len(sortedA) and sortedA[j] + sortedA[k] > sortedA[i]: 
                        #print(sortedA[j],sortedA[k],sortedA[i]);
                        return sortedA[j] + sortedA[k]+ sortedA[i];

        return 0;

    #一開始搞錯題目意思 還傻傻用三個迴圈  導致

    #但這題利用  兩邊和大於第三邊 的定理
    # 我們先把陣列排序過 直接從最大的數值開始檢查起  就可以找到面積最大的
```

之前卡在一個問題:

1,2,3,4, 8, 16

3, 4, 8 已經不行了  3, 4, 16 還有需要考慮嗎?

5 4 3 2 1 一樣也有這狀況

5, 4, 3不行 5,4,2就不用檢查了~

網友[chachazero](https://leetcode.com/chachazero)  也有另外附註

[https://leetcode.com/problems/largest-perimeter-triangle/discuss/218014/python-sort-and-check/221549](https://leetcode.com/problems/largest-perimeter-triangle/discuss/218014/python-sort-and-check/221549)

Hi,  
You don't have to check all combinations if you've sorted them.  
Because we only want "the largest" perimeter, we check from the longest length to the smallest length.  
When we find a valid triangle, it would be our answer!

You can think about a simple problem:  
How can we find three numbers in an array and their sum would be the biggest among any other sum of three numbers?  
If we sort them from big to small, the most left three numbers is the answer.  
How do we find the second biggest sum? It should be the 2nd, 3rd and 4th numbers and so on.

Then think about the original problem like this:  
How do we find the three numbers in an array and their sum would be the biggest, and they can form a triangle?  
It's just like the above simple problem, and when the biggest sum can't form a triangle, we go check the second biggest sum and so on.  
This way we only have to use one loop.  
The time complexity is O\(NlogN\) becasue we used sort\(\).

If you see the problem description, it says:  
3 &lt;= A.length &lt;= 10000

Most of the time when the test case is more than 10000, you want to find a solution which is better than O\(N^2\).  
You used 3 loops and it will be O\(N^3\)

Hope this help!



這邊ujhuyz0110   有另一份說明

https://leetcode.com/problems/largest-perimeter-triangle/discuss/219076/Python3-Beat-100.0





