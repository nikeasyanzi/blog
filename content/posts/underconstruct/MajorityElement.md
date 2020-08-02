# [3. Array/String](/arraystring.md)

# 169. Majority Element
https://leetcode.com/problems/majority-element/description/

```python
class Solution:
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        count=1;
        final=nums[0];    #final is candidate
        for i in range(1,len(nums)):
            if final ==nums[i]:
                count=count+1;
            else:
                count=count-1;
                if count==0:
                    final=nums[i];
                    count=1;
        return final;
```

基本上就是投票法囉   
因為至少出現n/2 次  
所以 如果下個element == candidate  則count +1
        否則count-1   
        最後count=0   表示candiate該被取代
    
    
# 229. Majority Element II
https://leetcode.com/problems/majority-element-ii/description/
