
# [6. Binary Search](/binarysearch.md)

## 4. Median of Two Sorted Arrays


```c

double findMedianSortedArrays(int* nums1, int nums1Size, int* nums2, int nums2Size) {
      const int n1 = nums1Size;
        const int n2 = nums2Size;
        // Make sure n1 <= n2
        if (n1 > n2) return findMedianSortedArrays(nums2,n2 , nums1,n1);
        
        const int k = (n1 + n2 + 1) / 2;
 
        int l = 0;
        int r = n1;
               
        while (l < r) {
            const int m1 = l + (r - l) / 2;
            const int m2 = k - m1;
            if (nums1[m1] < nums2[m2 - 1])
                l = m1 + 1;
            else
                r = m1;
        }
        
        const int m1 = l;
        const int m2 = k - l;
        
        const int c1 = (m1 <= 0 ? INT_MIN : nums1[m1 - 1])>(m2 <= 0 ? INT_MIN : nums2[m2 - 1])?(m1 <= 0 ? INT_MIN : nums1[m1 - 1]):(m2 <= 0 ? INT_MIN : nums2[m2 - 1]); // index excessed 
 
        if ((n1 + n2) % 2 == 1)
            return c1;    
        
        const int c2 = (m1 >= n1 ? INT_MAX : nums1[m1])>(m2 >= n2 ? INT_MAX : nums2[m2])?(m2 >= n2 ? INT_MAX : nums2[m2]):(m1 >= n1 ? INT_MAX : nums1[m1]);   // index excessed 
                
        return (c1 + c2) *0.5;
    }
    
1. 討論 新的 ck-1 ck  
    
    
```    
https://leetcode.com/problems/median-of-two-sorted-arrays/submissions/1

http://zxi.mytechroad.com/blog/algorithms/binary-search/leetcode-4-median-of-two-sorted-arrays/





