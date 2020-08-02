# [2. Math](/math.md)

## 7. Reverse Integer

[https://leetcode.com/problems/reverse-integer/description/](https://leetcode.com/problems/reverse-integer/description/)

```
Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

Input: 123
Output: 321
Example 2:

Input: -123
Output: -321
Example 3:

Input: 120
Output: 21
```

```c
#include <math.h>
#include <limits.h>
    int reverse(int x) {

    int count=0;
    int result=0;
    while(x!=0)
    {
        if(abs(result)>INT_MAX/10) return 0;// check if it will overflow after reverse 
        result=result*10+x%10;
        x=x/10;
    } 
    return result;
    }
```

這題真的很妙  這解法是官方解法 有幾個地方可以注意

1.不須考慮正負號 while 判斷式改成  x!=0  
因為不管x 正負,一直除下去,最後餘數會歸零

2.if判斷式   
用於事先的overflow 檢查  
if\(abs\(result\)&gt;INT\_MAX\)  但寫這樣是查不出來的

測資:  
1534236469  \(用於overflow偵測\)

Reference:  
[http://www.cnblogs.com/grandyang/p/4125588.html](http://www.cnblogs.com/grandyang/p/4125588.html)

在贴出答案的同时，OJ还提了一个问题 To check for overflow/underflow, we could check if ret &gt; 214748364 or ret &lt; –214748364 before multiplying by 10. On the other hand, we do not need to check if ret == 214748364, why? （214748364 即为 INT\_MAX / 10）

为什么不用check是否等于214748364呢，因为输入的x也是一个整型数，所以x的范围也应该在 -2147483648～2147483647 之间，那么x的第一位只能是1或者2，翻转之后res的最后一位只能是1或2，所以res只能是 2147483641 或 2147483642 都在int的范围内。但是它们对应的x为 1463847412 和 2463847412，后者超出了数值范围。所以当过程中res等于 214748364 时， 输入的x只能为 1463847412， 翻转后的结果为 2147483641，都在正确的范围内，所以不用check。

這邊再講甚麼 不是很懂!!!!!

Leet code 官方的解釋:  
因為  
$$ \text{INT_MIN} =    –2147483647 – 1 $$  
$$ \text{INT_MAX} =    2147483647 $$

To explain, lets assume that  is positive.

If $$temp = \text{rev} \cdot 10 + \text{pop} $$ causes overflow, then it must be that $$\text{rev} \geq \frac{INTMAX}{10}$$  
​  
If $$\text{rev} > \frac{INTMAX}{10}$$ , then $$ temp = \text{rev} \cdot 10 + \text{pop}$$ is guaranteed to overflow.  
If $$ \text{rev} == \frac{INTMAX}{10} $$, then $$ temp = \text{rev} \cdot 10 + \text{pop}$$ will overflow if and only if $$ \text{pop} > 7$$

Similar logic can be applied when $$ \text{rev}$$ is negative.

when $$rev$$ is negative  
If $$\text{rev} < \frac{INTMIN}{10}$$ , then $$ temp = \text{rev} \cdot 10 + \text{pop}$$ is guaranteed to overflow.  
If $$ \text{rev} == \frac{INTMIN}{10} $$, then $$ temp = \text{rev} \cdot 10 + \text{pop}$$ will overflow if and only if $$ \text{pop} < -8$$

所以pop 需分別檢查   7 or -8

```c++
class Solution {
public:
    int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int pop = x % 10;
            x /= 10;
            if (rev > INT_MAX/10 || (rev == INT_MAX / 10 && pop > 7)) return 0;
            if (rev < INT_MIN/10 || (rev == INT_MIN / 10 && pop < -8)) return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
};
```

[https://leetcode.com/articles/reverse-integer/](https://leetcode.com/articles/reverse-integer/)

