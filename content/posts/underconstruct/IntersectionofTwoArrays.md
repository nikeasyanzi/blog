# [3. Array/String](/arraystring.md)

### 349. Intersection of Two Arrays
https://leetcode.com/problems/intersection-of-two-arrays/description/

這題是用O(n)的解法

直接查表

```python
class Solution:
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        result=[];
        
        for i in nums1:
            if i in nums2 and i not in result:
                result.append(i);
            
        return result;

```

### 350. Intersection of Two Arrays II

https://leetcode.com/problems/intersection-of-two-arrays-ii/description/

這題是要回傳共同有的元素  而且相同數量

作法:
1.依序pop 在array1的每個元素
如果該元素存在array2 
則push 回去 array1

2.此時 如果該元素存在array2  也要把該元素從array2移除
確保數量會一樣


test case:
[2,1]
[1,1]

return [1]

[1,2,2,1]
[2]

return [2]

[2,1]
[1,2]

return [1,2]


```python
class Solution:
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        
        if nums1==[] or nums2==[]:
            return [];
        length=len(nums1);
        
        for i in range(length):
            #print(length);
            #print(nums1);
            val=nums1.pop(0);
            #print(val);
            if val in nums2:
                nums2.pop(nums2.index(val));
                nums1.append(val);
                    
        return nums1;
```