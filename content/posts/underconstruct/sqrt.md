# [\# 2.Math](/math.md)

# 69. Sqrt\(x\)

[https://leetcode.com/problems/sqrtx/submissions/1](https://leetcode.com/problems/sqrtx/submissions/1)



1. 開根號的背景說明

求開根號 可以用f\(x\)=x^2  求 x

則  1 &lt; x &lt; \(x^2\)/2

所以我們可以用binary search 搜尋

但說穿了 面試最好記的  
還是2分搜尋區間\[1,x/2\]

```c
 while (high - low > small)  // 不斷逼近，直到範圍夠小為止。
    {
      double mid = (low + high) / 2;
      if (mid*mid > x)          // 解小於 mid , 將上限調為 mid
        high = mid;
      else
        low = mid;              // 解大於 mid , 將下限調為 mid
    }
    return low;
```

2.但牛頓法式目前已知最快  除了 quack III 的magic code

這邊針對牛頓法原理說明一下

函數可以改寫成  f\(x\)=x^2-y=0  
後面看不懂  嗚嗚

```c
int mySqrt(int x) {
    if (x<=1) return x;

    double last = 0;
    double res = 1;
    while (res != last)
    {
        last = res;
        res = (res + x / res) / 2;
    }
    return (int)res;
}
```

[https://baike.baidu.com/item/牛顿迭代法](https://baike.baidu.com/item/牛顿迭代法)

[https://blog.csdn.net/ycf74514/article/details/48996383](https://blog.csdn.net/ycf74514/article/details/48996383)

[http://www.cnblogs.com/AnnieKim/archive/2013/04/18/3028607.html](http://www.cnblogs.com/AnnieKim/archive/2013/04/18/3028607.html)

