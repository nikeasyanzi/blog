# [3. Array/String](/arraystring.md)

# 26. Remove Duplicates from Sorted Array

    
    Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.
    
    Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
    
    Example 1:
    
    Given nums = [1,1,2],
    
    Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
    
    It doesn't matter what you leave beyond the returned length.
    Example 2:
    
    Given nums = [0,0,1,1,1,2,2,3,3,4],
    
    Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.
    
    It doesn't matter what values are set beyond the returned length.  
    
      
      
  
 [123](/questions/MoveZeroes.md)
 這題跟 [move zero](/questions/MoveZeroes.md) 很像 兩個指標就可以完成  
  
```c
  void swap(int *a,int *b){
    //printf("*a=%d,*b=%d\n",*a,*b);   
    if(*a!=*b){
        *a^=*b;
        *b^=*a;
        *a^=*b;
    }
    //printf("*a=%d,*b=%d\n",*a,*b);   
}

int removeDuplicates(int* nums, int numsSize) {
    int *ptr =nums;
    int i=0;
    int j=1;
    int target=nums[i];
    if (numsSize==0) return 0;
    while( j<numsSize){
        //printf("i=%d,j=%d,target=%d\n",i,j,target);
        if(target<nums[j]){
            i++;
            swap(&nums[i],&nums[j]);
            target=nums[i];
        }
        j++;
    }  
    //printf("i=%d",i);
    return i+1; // return the number of distinct numbers
 
}
```
  
  https://leetcode.com/submissions/detail/153996226/

i, j, & target
目標是  j loop over the whole array and 找 一個大於target的值
tast case:

[1, 1, 2, 3]

[1,1,1,2,2,2,3,3,4,4]






# 80. Remove Duplicates from Sorted Array II
    Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.
    
    Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
    
    Example 1:
    
    Given nums = [1,1,1,2,2,3],
    
    Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.
    
    It doesn't matter what you leave beyond the returned length.
    Example 2:
    
    Given nums = [0,0,1,1,1,1,2,3,3],
    
    Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.
    
    It doesn't matter what values are set beyond the returned length.

https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/
       
```c
int removeDuplicates(int* nums, int numsSize) {    
    int count=0;
    int i=0;
    while(i<numsSize){ 
        if (count<2 || nums[count-2]!=nums[i]){
            nums[count]=nums[i];
            count++;
        }
        i++;
    }
    return  count;
}
```

https://leetcode.com/submissions/detail/155672597/

the fatest sol:
'''c
int removeDuplicates(int* nums, int numsSize) {
    if(numsSize<3)return numsSize;
    int cnt = 2;
    int nums1[numsSize];
    memcpy(nums1,nums,numsSize*sizeof(int));
    for(int i=2;i<numsSize;i++){
        if(nums1[i] > nums1[i-2])
            nums[cnt++] = nums1[i];
        else
            continue;
    }
    return cnt;
}
```
Reference: 
https://shenjie1993.gitbooks.io/leetcode-python/080%20Remove%20Duplicates%20from%20Sorted%20Array%20II.html

