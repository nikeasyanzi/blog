# [# 3.Array/String](/arraystring.md) *

題目
448. Find All Numbers Disappeared in an Array

https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:

Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]




解題:

本來是想說 遍彷每個元素i    並把 元素值-1  當idx 並 把對應的元素 變負  O(n)
之後再遍彷每個元素  找負數  即可

見下圖

|i | [4,3,2,7,8,2,3,1] 
|---|--- 
|0 | [4,3,2,**-7**,8,2,3,1] 
|1 | [4,3,**-2**,-7,8,2,3,1] 
|2 | [4,**-3**,-2,-7,8,2,3,1] 
|3 | [4,-3,-2,-7,8,2,**-3**,1] 
|4 | [4,-3,-2,-7,8,2,-3,**-1**]  
|5 | [4,-3,-2,-7,8,2,-3,-1]  
|6 | [4,-3,-2,-7,8,2,-3,-1] 
|7 | [**-4**,-3,-2,-7,8,2,-3,-1] 



https://leetcode.com/submissions/detail/153162749/


```go
func abs(n int) int {
    y := n >> 31
    return (n ^ y) - y
}

func findDisappearedNumbers(nums []int) []int {

    i := 0
    for i < len(nums) {

        if nums[abs(nums[i])-1] > 0 {
            nums[abs(nums[i])-1] = -nums[abs(nums[i])-1]
        }
        i++
    }

    i = 0
    var j int
    j = 0
    slice := make([]int, 0)

    //fmt.Printf("1i =%d , j=%d, len(nums)=%d \n", i, j, len(nums))
    for i < len(nums) {
        //fmt.Printf("2i =%d , j=%d, len(nums)=%d \n", i, j, len(nums))
        if nums[i] > 0 {
            slice = append(slice, i+1)
            //fmt.Printf("ans %d \n", i+1)
            j++
        }
        i++
    }

    fmt.Println("slice:", slice)
    return slice
}
```

下面Leetcode上 最快的 別人的寫法
有夠簡單   不用去管 正負  但當然要多使用了一點記憶體

看完有種恍然大悟的感覺


```go
func findDisappearedNumbers(nums []int) []int {
    
    var a []int
    for i := 0; i < len(nums) + 1; i++ {
        a = append(a, 0)
    }
    
    for i := 0; i < len(nums); i++ {
        a[nums[i]] = 1
    }

    var ans []int
    for i := 1; i < len(a); i++ {
        if a[i] == 0 {
            ans = append(ans, i)
        }
    }
    return ans
}
```

## 總結:
1.
func abs(n int) int {
    y := n >> 31
    return (n ^ y) - y
}

這種求abs 不需要brach  會比較快

2.
這種數字陣列系列的題目  通常都可以用index & element value 來操作求解