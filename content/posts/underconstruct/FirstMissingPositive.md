# [3.Array/String](/arraystring.md)

# [ 41. First Missing Positive ](/questions/FindMissingPositive.md)

https://leetcode.com/problems/first-missing-positive/description/

Given an unsorted integer array, find the smallest missing positive integer.

Example 1:

Input: [1,2,0]
Output: 3
Example 2:

Input: [3,4,-1,1]
Output: 2
Example 3:

Input: [7,8,9,11,12]
Output: 1

```go
func swap(a *int, b *int) {
    //  fmt.Printf("1a=%d b=%d \n", *a, *b)
    if *a != *b {
        *a ^= *b
        *b ^= *a
        *a ^= *b
    }
    //  fmt.Printf("2a=%d b=%d \n", *a, *b)
}

func firstMissingPositive(nums []int) int {
    i := int(0)
    for i < len(nums) {
        fmt.Printf("i=%d \n", i)
        if nums[i] <= len(nums) && nums[i] > 0 && nums[i]-1 != i && nums[i] !=nums[nums[i]-1] {
            fmt.Println(nums)
            fmt.Printf("swap a=%d b=%d \n", nums[nums[i]-1], nums[i])
            swap(&nums[nums[i]-1], &nums[i])
        } else {
            i++
        }
    }

    i = 0
    for i < len(nums) {
        if nums[i]-1 != i {
            break
        }
        i++
    }
    //fmt.Println(nums)
    //fmt.Printf("%d ", i+1)
    return i + 1
}
```
解題:

1. 找最小正數  範圍為 1-n, index range = 0 - n-1

2. 基本上是  遍巡每個element   並把  element 換到 element -1 的位置  
一直換就好   但注意  換不到位還是要繼續換  所以 只有if 不成立 i才會++ (見圖解 i=2)

3. 注意nums[i] !=nums[nums[i]-1] 
因為測資可能是[1,1]

4. 最後一行是  萬一大家都一樣  ex. [1,2,3,4] 則回傳5 
圖解 

|i | [3,4,-1,1]
|---|---
|0 | [-1,4,3,1]
|1 | [-1,1,3,4]
|  | [1,-1,3,4]
|2 | pass
|3 | pass


複雜度分析   每swap 一次  至少 1個element   到達正確位置   所以為O(n)
