
#[7.Bit Manipulation](/bit-manipulation.md)

##[136. Single Number](https://leetcode.com/problems/single-number)

這題其實就是用XOR

The characteristic of XOR operation is when x ^ x =0, x ^ ~x =1

giving a set of numbers a,b,c,d,e, ... ,x,y,z while z is the one which appears onces and others appear twices

it can be expressed as follows:

a ^b.... ^x ^y ^z ^a ^b ... ^x ^y
=a ^a ^b ^b ... ^x ^x ^y ^y ^z
=0 ^0 ... ^0 ^ z
=z

##[137. Single Number II](https://leetcode.com/problems/single-number-ii/)

```c
int singleNumber(int* nums, int numsSize) {
    int num=0;
    int i=0;
    int appear_one=0;
    int appear_two=0;
    int appear_three=0;

    for (i=0; i<numsSize; i++) {
        appear_two|=appear_one&nums[i];
        appear_one^=nums[i];
        appear_three=appear_one& appear_two;
        appear_one &= ~ appear_three;
        appear_two &= ~ appear_three;
    }
    return appear_one;  
}
```



> 这个解法可以初学者会看不明白，详细说明一下：  
> 1）有个数只出现一次，换个思考角度表达，用二进制的思考，即二进制每一位上都有一个数只出现一次  
> 那对上面三个数1、2、1（简单为例子使用4位表示）：  
> 0,0,0,1  
> 0,0,1,0  
> 0,0,0,1
>
> 第一位：1,0,1
>
> 第二位：0,1,0
>
> 第三位：0,0,0
>
> 第四位：0,0,0
>
> 2）我们使用三个变量one、two、three来存储每一个位上出现的1、2、3次的情况（其实是模拟了3进制的概念），拿第一位思考（特别注意one、two、three的每一位，都表示当前位出现了1次）  
> 使用上面的第一位的序列1,0,1为例子
>
> 3）因此，"拼凑"出的算法就是
>
> two = two \| \(one & num\[i\]\)  // this  appears ahead of one=one^num\[i\] since a bug occurs when a new muber comming in
>
> one = one ^ num\[i\]
>
> three = one & two
>
> one = ~three
>
> two = ~three

[https://www.jianshu.com/p/758e799614b2](https://www.jianshu.com/p/758e799614b2)



## [260. Single Number III](https://leetcode.com/problems/single-number-iii/)

這題其實事Single Number的進階  還沒時間看

[https://segmentfault.com/a/1190000004886431](https://segmentfault.com/a/1190000004886431 "leetcode 算法解析（一）：260. Single Number III")

[http://fisherlei.blogspot.com/2015/10/leetcode-single-number-iii-solution.html](http://fisherlei.blogspot.com/2015/10/leetcode-single-number-iii-solution.html)





