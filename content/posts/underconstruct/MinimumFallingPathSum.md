# [3. Array/String](/arraystring.md)


[931. Minimum Falling Path Sum](https://leetcode.com/problems/minimum-falling-path-sum/)

Dynamic programming

這題看了其他網友的做法  豁然開朗
參照reference的圖片
![](/assets/MinimumFallingPathSum.png)

可發現
3*3的minimum 可由2*2的minimum推導而來  為divide and conquer 
利用dyanmic programming memorization的技巧即可解出

做法:

* 先在最左與最右兩行加入value 為int_max 的element
* 此時只要從index =1 row 開始 計算 minimum 直到最後
* 最後一個row 的min 即為所求 global min


```python
class Solution:
    def minFallingPathSum(self, A):
        """
        :type A: List[List[int]]
        :rtype: int
        """
        matrix= [[0 for x in range(len(A[0])+2)] for y in range(len(A[0]))];
    
        for i in range(len(A[0])):    #here we fill the append column with INT max.
            matrix[i][0]=sys.maxsize;
            matrix[i][len(A)+1]=sys.maxsize;
        
        for i in range(len(A[0])):
            for j in range(len(A[0])):
                matrix[i][j+1]=A[i][j];

        #print (matrix);
      
        for i in range(1,len(A[0])):
            for j in range(1,len(A[0])+1):
                    #print (matrix);
                    #print("i=",i,"j=",j,"matrix[i-1][j-1]=",matrix[i-1][j-1],"matrix[i-1][j]=",matrix[i-1][j],"matrix[i-1][j+1]=",matrix[i-1][j+1]);
                    matrix[i][j]=min(matrix[i-1][j-1], matrix[i-1][j],matrix[i-1][j+1])+matrix[i][j];
        #print (matrix);
        
        #global min is the minimum of the last row
        #print(min( [matrix[len(A[0])-1][j] for j in range(1,len(A[0]) +1 )]));
        return min( [matrix[len(A[0])-1][j] for j in range(1,len(A[0]) +1 )]);  
"""
test case
[[51,24],[-50,82]]
[[1,2,3],[4,5,6],[7,8,9]]

"""

```

#Reference:
https://leetcode.com/problems/minimum-falling-path-sum/discuss/186689/Java-DP-solution-with-graph-illustrated-explanations