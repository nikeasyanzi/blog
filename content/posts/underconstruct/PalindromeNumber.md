# [2. Math](/math.md)
## 9. Palindrome Number

https://leetcode.com/problems/palindrome-number/description/

    Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
    
    Example 1:
    
    Input: 121
    Output: true
    Example 2:
    
    Input: -121
    Output: false
    Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
    Example 3:
    
    Input: 10
    Output: false
    Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
    

```c
bool isPalindrome(int x) {
    if (x<0) return false;
        int y=0;
        int tmp=x;
    while(tmp){
        y=y*10+tmp%10;
        if(y>INT_MAX) {printf("overflow\n"); return false;} //overflow ex. 2^32 = 2,147,483,647 
        tmp=tmp/10;
    }
        printf("y=%d\n",y);
        
    if(y==x) return true;
    
    return false;
}
```


even for 2^32  2,147,483,647 , you get
y=-1126087180

that means not equal and leads to a correct answer in this case.

so, I think it's fine to not to do overflow detection