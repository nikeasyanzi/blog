# [2. Math](/math.md)

## 371. Sum of Two Integers
https://leetcode.com/problems/sum-of-two-integers/description/

    Calculate  the sum of two integersaandb, but you arenot allowedto use the operator+and-.
    Example:
    Given a= 1 and b= 2, return 3.


```c
int getSum(int a, int b) {
    int sum; 
    int carry;
    if (a==0) return b;
    if (b==0) return a;
    
    while(b!=0){    
        carry=a& b;
        a=a^b;
        b=carry<<1;
    }
    return a;
}
```
