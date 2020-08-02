# [3. Array/String](/arraystring.md)

[## 560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

```python
class Solution:
    def subarraySum(self, nums, k):
        result, cur_sum = 0, 0
        sum_dict = {0:1}
        for num in nums:
            cur_sum += num    //recording the prefix sum
            if cur_sum - k in sum_dict:
                result += sum_dict[cur_sum - k]
            if cur_sum in sum_dict:
                sum_dict[cur_sum] += 1
            else:
                sum_dict[cur_sum] = 1
                
        return result
```

也可以用collection 的作法
```python        
class Solution:
    def subarraySum(self, nums, k):
        mydict = collections.Counter()
        curr_sum=0;
        ans=0;
        for i in range(len(nums)):
            mydict[curr_sum]= mydict[curr_sum]+1;
            curr_sum=curr_sum+nums[i];
            #print (mydict);
            ans=ans+mydict[curr_sum-k];
        return ans;
```

### 說明

其實這題可以利用prefix sum

denote the sum between i,j as

$$
sum(i,j) = sum(0,j) - sum(0,i)
$$

$$
k = sum(0,j) - sum(0,i)
$$

所以我們可以用一個hash map 紀錄 prefix sum 出現的次數  (代表sum[0,i])

那每次疊代

* 當前的Prefix sum 次數+1
* 更新prefix sum (代表 sum[0,j])
* 更新ans by ans= ans + hash[k-prefix_sum], 

### Reference:
   * https://leetcode.com/problems/subarray-sum-equals-k/discuss/102106/Java-Solution-PreSum-%2B-HashMap
   * https://leetcode.com/problems/subarray-sum-equals-k/discuss/164431/Python-or-3-tm
   * https://zxi.mytechroad.com/blog/hashtable/leetcode-560-subarray-sum-equals-k/
  
  這篇解釋了prefix sum的
* https://leetcode.com/problems/binary-subarrays-with-sum/discuss/186647/Java-Clean-Solution-2-Sum-%2B-Prefix-Sum-Caching

## [713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)

說明:
這題也是類似prefix的概念 外加sliding window

我們每次紀錄目前的product 與 index i

如果product > k 則開始除去前面的數 index j


```python
    class Solution:
        def numSubarrayProductLessThanK(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        product=1;
        j=0;
        res=0;
        if k==0: # if k==0, the result is zero
            return 0;
        for i in range(len(nums)):
            product=product*nums[i];
        #print("product=",product);
        while product>=k and j< len(nums): # be careful with         the condition j< len(nums)
            product=product/nums[j];
            j=j+1;

        #print("j=",j,"i=",i,"i-j+1=",i-j+1);
        if product<k:
            res= res+ i-j+1 ;
        #print(res);
        return res;
```

https://buptwc.github.io/2018/10/28/Leetcode-930-Binary-Subarrays-With-Sum/


## [930. Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum/)
這題其實也可以用560. Subarray Sum Equals K 的概念去做 
 
```python
class Solution:
    def numSubarraysWithSum(self, A, S):

       # c = collections.Counter({0: 1})  #memoization dictionary and key '0' is valued at '1' as we count the case when psum==S, we can also add this with res

       # print(c);
        #psum = res = 0
       # for i in A:
       #     psum += i  # This basically checks the sum as we traverse the list
      #      res += c[psum - S] # This is keeping track of when we get past S, as when we get past S, we start with the new substring, and we already have the count and use it when we reach the SUM again and again
            
       #     c[psum] += 1
      #  print(c);
        #return res
        mydict = collections.Counter()
        curr_sum=0;
        ans=0;
        for i in range(len(A)):
            mydict[curr_sum]= mydict[curr_sum]+1;
            curr_sum=curr_sum+A[i];
            #print (mydict);
            ans=ans+mydict[curr_sum-S];
        
        return ans;
```    
  或者 利用一個index array 紀錄當前為1的element 的count
     
```python
class Solution(object):
    def numSubarraysWithSum(self, A, S):
        if not A: return 0
        index = [-1]
        for i in range(len(A)):
            if A[i] == 1: index.append(i)
        index.append(len(A))

        res = 0
        if S == 0: # 单独处理S = 0的情况
            for i in range(1, len(index)):
                num = index[i] - index[i-1] - 1
                res += (num+1)*num // 2
            return res
        # 从index = 1开始遍历
        i,j = 1,1
        while i < len(index)-1:
            j = i + S
            if j >= len(index): break
            res += (index[i]-index[i-1]) * (index[j]-index[j-1])
            i += 1
        return res
```


Example:  [1,0,1,0,0,1]

    index array=[-1,0,2,2,5,6]
    
i| j| expression      
----|---------- 
1| 3| 0-(-1)*(5-2)=3
2| 4| (2-0)*(6-5)=2

很明顯這演算法在S=0 是不能使用   
所以只能另外計算
    
Reference:
https://blog.csdn.net/fuxuemingzhu/article/details/83478995
http://hehejun.blogspot.com/2018/10/leetcodebinary-subarrays-with-sum.html
https://buptwc.github.io/2018/10/28/Leetcode-930-Binary-Subarrays-With-Sum/
https://www.youtube.com/watch?v=eRx56MI3Svo


# 类似题目：
### Two Sum

### Continuous Subarray Sum

### Subarray Product Less Than K

### Find Pivot Index
