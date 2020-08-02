
# [2. Math](/math.md)

# [400. Nth digit](https://leetcode.com/problems/nth-digit/)

```python
class Solution:
    def findNthDigit(self, n):
        """
        :type n: int
        :rtype: int
        """
        count=1;    #number of digits of each number in this level
        base=9;   
        curr_length=base* (10 **(count-1))*count# total number of digits in this level    
        start=1;
        while n > curr_length:
            n=n-curr_length;
            start=start+base* (10 **(count-1));
            count=count+1;
            curr_length=base* (10 **(count-1))*count; 
            #print("start=",start);
            #print("start=",start,"count=",count,"curr_length=",curr_length,"n=",n);
            
        off= (n-1)/(count);
        idx=(n-1)%(count); 
        #print("off=",off,"idx=",idx);
        
        return  int(str(start+off)[idx]);

```
| count number of digits in this level  |   1    | 2  | 3
|----------|:-------------:|------:|
| numbers in this level (9* 10^count-1)  |  9   | 90 | 900
|curr_length (9* (10^count-1) * count )| 9   | 180| 2700
|start number in this level | 1 | 10 | 100

說明:
1. 仔細觀察會發現
    
    1位數的數字有9個    1-9
    2位數的數字有90個  10-99
    3位數的數字有900個 100-999

    所以我們用count 來記錄位數
2. 最後 剩下不足的部分用count來除  代表offset

3. 餘數的部分  就是該數字的第幾位囉
        
4. 為什麼計算offset and idx 要n-1 因為  我們start 是從第一個數開始 (第一個數也包含)


ex. 100

|count|1|2
|---|:---:|---:|
|curr_length|9|180(90*2)
|n|100-9=91|
|start|1|10
|offset||(91-1)/2=45
|idx||(91-2)%2=0
|ans||10+45 = "5"5

# Reference: 
* Leetcode | 400 | Nth Digit | Java   
https://www.youtube.com/watch?v=VKYnABegaEI

https://leetcode.com/problems/nth-digit/discuss/182837/C%2B%2BCJava-5-line-O(1)-solution-no-strings-no-loopsrecursion-with-explanation

