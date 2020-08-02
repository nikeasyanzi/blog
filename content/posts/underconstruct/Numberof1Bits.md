##[7.Bit Manipulation](/bit-manipulation.md)

##[191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/submissions/1)

這題就是計算 一個數 有幾個bit 是1

```c
int hammingWeight(uint32_t n) {
    int count=0;
    while(n>0){
        count=count+(n & 1);
        n=n>>1;
    }
    return count;
}
```
