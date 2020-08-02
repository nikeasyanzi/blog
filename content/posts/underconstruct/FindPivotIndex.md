
# [# 3.Array/String](/arraystring.md)


## 724. Find Pivot Index


https://leetcode.com/problems/find-pivot-index/description/
Given an array of integers nums, write a method that returns the "pivot" index of this array.

We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.

If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.

Example 1:
Input: 
nums = [1, 7, 3, 6, 5, 6]
Output: 3
Explanation: 
The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.
Also, 3 is the first index where this occurs.



流程:
1.計算total sum
2.loop over the array 然後逐一減去  再比較左右兩邊

當初一開始想說  直接由右往左移  
後來發現 規定要回傳left most
改直接由左往右移

```go
func pivotIndex(nums []int) int {
    i := 0
    left := 0
    right := 0
    for i < len(nums) {    //calculate total sum
        right = right + nums[i]
        i++
    }

    i=0;
    for i<len(nums) { 
        left = left + nums[i]

        //fmt.Println("right=%d,left=%d, %d", right, left, j)
        if right == left {
            return i
        }
        right = right - nums[i]        
        i++
    }
    return -1
}
```

https://leetcode.com/submissions/detail/153135834/