
# 3.Array/String [](/arraystring.md)

# 665. Non-decreasing Array

https://leetcode.com/problems/non-decreasing-array/description/

    Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.
    
    We define an array is non-decreasing if array[i] <= array[i + 1] holds for every i (1 <= i < n).
    
    Example 1:
    Input: [4,2,3]
    Output: True
    Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
    Example 2:
    Input: [4,2,1]
    Output: False
    Explanation: You can't get a non-decreasing array by modify at most one element.
    Note: The n belongs to [1, 10,000].


https://leetcode.com/submissions/detail/153862262/

# 最速解
```go   
func checkPossibility(nums []int) bool {
 
    var count int;
    i:=1;
    
    for i<len (nums){
        if(nums[i-1]>nums[i]){
            if (i-1==0){
                nums[i-1]=nums[i]
            }else{
                if (nums[i]<nums[i-2]){
                    nums[i]=nums[i-1]
                }else{
                    nums[i-1]=nums[i]
                }
            }
            count++;
            if count ==2{ return false;}
        }    
        i++;
    }
    return true;
}
```

#第二種解法

```Go
func checkPossibility(nums []int) bool {
 
    var count int;
    i:=1;
    
    for i<len (nums){
        if(nums[i-1]>nums[i]){
            if (i-1!=0 && nums[i]<nums[i-2]){
                nums[i]=nums[i-1]
            }else{
                nums[i-1]=nums[i]
            }
            count++;
            if count ==2{ return false;}
        }    
        i++;
    }
    return true;
}
```
說明:
這題其實是要考慮 前一位, 當前位 跟後一位的關係 

假設考慮當前 i=2   則

test case:

[2,4,2,6] -> [2,2,4,6]

[3,4,2,6] -> [X]  無法替換 因為  num[i+1] < num[i-1]

[2,4,3,6] -> [2,3,4,6]

[3,2,4,6] -> [2,3,4,6]


http://nirajsdatabase.blogspot.tw/2017/08/given-array-with-n-integers-your-task.html


### 896. Monotonic Array

https://leetcode.com/contest/weekly-contest-100/problems/monotonic-array/

```c
bool isMonotonic(int* A, int ASize) {
    int increase=1;
    int decrease=1;
    int i=0;
    if (ASize <=2){
        return true;    
    }
    
    for (i=1;i<ASize;i++){
        increase =increase &( A[i - 1] <= A[i]);
        decrease &= (A[i - 1] >= A[i]);
    }       
    return increase||decrease;
}
```

