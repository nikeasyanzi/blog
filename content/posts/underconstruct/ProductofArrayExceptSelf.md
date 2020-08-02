# [3.Array/String](/arraystring.md)


# 238. Product of Array Except Self

    Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].
    
    Example:
    
    Input:  [1,2,3,4]
    Output: [24,12,8,6]
    Note: Please solve it without division and in O(n).
    
    Follow up:
    Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)


https://leetcode.com/problems/product-of-array-except-self/description/
    
    
    
```c
    int* productExceptSelf(int* nums, int numsSize, int* returnSize) {
    
    int i=0;
    int count=-1;
    int p;
    int *result=malloc(sizeof(int)*numsSize);
    
    *returnSize=numsSize;
    p=1;
    result[0]=1;
    for(i=1;i<numsSize;i++){
        result[i]=nums[i-1]*result[i-1];
    }   
    
    p=1;
    for(i=numsSize-2;i>=0;i--){
        p=p*nums[i+1]; //use p to save the memory space
        result[i]=p*result[i];
    }
    
    //for(i=0;i<numsSize;i++){
    //    printf("%d ",result[i]);
    //}
    
    return result; 
}
    
```
https://leetcode.com/submissions/detail/155201886/



說明: 

1. 直觀的寫法其實是 $$ a[i]= \prod/a[i]$$
但這題不能用除法

2. 所以 假設一個陣列
 $$ [a0,a1,a2,a3] $$
 可以想成 
$$left=[1, a_0, a_0*a_1, a_0*a_1*a_2]$$
$$right=[a_1*a_2*a_3, a_2*a_3, a_2, 1 ]$$

 一般的做法是直接left *right

3. 但如果這時候再考慮 利用常數p 來存 right的結果 可節省記憶體

4. 有個特殊狀況可考慮
   
   1. 有一個element為0
   則最後結果 只有該elemet有值

   2. 有兩個element為0
   則最後結果全為0
   
   
  ![](http://3.bp.blogspot.com/-6KWF3HCWUGc/ViyGdIJ_7mI/AAAAAAAAMQI/9HH9PZvBtvM/s1600/Picture4.png) 

#reference
http://fisherlei.blogspot.com/2015/10/leetcode-product-of-array-except-self.html
