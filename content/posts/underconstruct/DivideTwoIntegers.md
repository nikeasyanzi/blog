#[7.Bit Manipulation](/bit-manipulation.md)
#29. Divide Two Integers
https://leetcode.com/problems/divide-two-integers/


```c=
int divide(int dividend, int divisor) {
    
    unsigned int dvs;
    unsigned int dvd;
    int res=0;
    
    if(divisor == 0 || (dividend == INT_MIN && divisor == -1))
        return INT_MAX;
    //here we record the sign first
    int sign= (dividend>0) ^ ( divisor >0)?-1:1;  //sign check
    //here we convert the two numbers into positive ones
    dvd=dividend <0?-dividend:dividend;
    dvs=divisor <0?-divisor:divisor;
    printf("sign=%d dvd=%u dvs=%u\n",sign,dvd,dvs);
    
    if(dvd < dvs) return 0;
    while (dvd >= dvs) { 
        long long temp = dvs, multiple = 1;
        while (dvd >= (temp << 1)) {
            temp <<= 1;
            multiple <<= 1;
        }
        dvd -= temp;
        res += multiple;
       //printf("dvd=%u,res=%u\n",dvd,res);
    }
    return sign==1?res:-res;
}
```

啟發:
92/3=30....2
92/3*2^4=1....44
44/3*2^3=1....20
20/3*2^2=1....8
8/3*2^1=1....1

quotion=2^4+2^3+2^2+2^1=30

作法:
1. sign check 要用xor
2. 接著就當作無號正整數來處理,
3. special case 要注意
*    1.因為 32bit 範圍是 -2^31 ~ 2^31-1
萬一 是 -2^31 / -1  要回傳2^31  會overflow 必須改成回傳INT_MAX
*    2.萬一除數是0,也是返回INT_MAX

另一種做法是:(保證只shift 32次)

we assure the factor ret's binary fomula is


$$
ret= a_{0} + a_{1} * 2^{1} + a_{2} * 2^{2} +...+ a_{31} * 2^{31}  where  a_{0} = 0 or 1
$$



the dividend B and divisor A is non-negative, then
$$
A (a_{0} + a_{1} * 2^{1} + a_{2} * 2^{2} +...+ a_{31} * 2^{31})=B  
$$


* (1) when Eq1 divided by$$ 2^{31}$$, we can get A*a31 = B>>31; then a31 = (B>>31)/A;

if (B>>31) > A, then a31 = 1; else a31 = 0;

* (2) when Eq1 divided by 2^30, we can get A*a30 + A*a31*2 = B>>30; then a30 = ((B>>30) - a31*A*2)/A; and (B>>30) - a31*A*2 can be rewritten by (B-a31*A<<31)>>30, so we make B' = B-a31*A<<31, the formula simplified to a30 = (B'>>30)/A

if (B'>>30) > A, then a30 = 1; else a30 = 0;

(3) in the same reason, we can get a29 = ((B-a31*A<<31-a30*A<<30)>>29)/A, we make B'' = B' - a30*A<<30, the formula simplified to a29 = (B''>>29)/A;

do the same bit operation 32 times, we can get a31 ..... a0, so we get the ret finally.


Reference:
https://leetcode.com/problems/divide-two-integers/discuss/13407/Detailed-Explained-8ms-C%2B%2B-solution

https://leetcode.com/problems/divide-two-integers/discuss/13420/32-times-bit-shift-operation-in-C-with-O(1)-solution

https://prismoskills.appspot.com/lessons/Bitwise_Operators/Efficient_Divide.jsp
