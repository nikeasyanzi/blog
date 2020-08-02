# [2. Math](/math.md)

## 66. Plus One

https://leetcode.com/problems/plus-one/description/

Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.


```c
int* plusOne(int* digits, int digitsSize, int* returnSize) {
    int i=digitsSize-1;
    int *result;
    int carry=1;
    int j=0;
    while (i>=0){
        digits[i]=digits[i]+carry;
        carry=digits[i]/10;  
        digits[i]=digits[i]%10;
        //printf("i=%d digit=%d,carry=%d\n",i, digits[i],carry);
        i--;   
    }
    //printf("\ncarry=%d\n",carry);
    
    //calculate returnSize
    *returnSize=digitsSize;
    if(carry==1) (*returnSize)++;
    
    result= malloc( sizeof(int) *(*returnSize) );

    //the final carry is the first element of the result
    if(carry==1){
        result[j]=carry;
        j++;    
    }
    
    i=0;
    while(i<digitsSize){
        result[j]=digits[i];
        //printf("%d ",result[j]);
        i++;
        j++;
    }
    return result;
}
```

https://leetcode.com/submissions/detail/150235765/


這題做法很直觀
直接拿原本的array 來處理(from right to left)  並額外記錄最後的carry即可

test case:
[0] -> [1]

[1,2,3] -> [1,2,4]

[9] -> [1,0]

