
## [3. Array/String](/arraystring.md)


## 125. Valid Palindrome

https://leetcode.com/problems/valid-palindrome/description/
    
    Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
    
    For example,
    "A man, a plan, a canal: Panama" is a palindrome.
    "race a car" is not a palindrome.

```c
int isAlphbat(char a)
{
    if((a>='a' && a<='z')||(a>='A' && a<='Z') )
    {
        return true;
    }
    return false;
}

int isDigit(char a)
{
    if((a>='0' && a<='9') )
    {
        return true;
    }
    return false;
}
int cmp(char a,char b)
{
    if(isAlphbat(a)&& isAlphbat(b))
    {
        if(a==b )
            return true;

        if((a>b && a-b=='a'-'A' ) || (a<b && b-a=='a'-'A'))
            return true;
    }
    else
    {
        if(isDigit(a)&& isDigit(b))
        {
            if(a==b )
                return true;
        }
    }
    return false;

}

bool isPalindrome(char *s)
{
    char *head=s;
    char *tail=head+strlen(s)-1;
    if (s==NULL)    //null case
    {
        return true;
    }
    while(head<tail)
    {
        while(!isAlphbat(*head) && !isDigit(*head))//get the first alphbat or digit
            head++;

        while(!isAlphbat(*tail) && !isDigit(*tail))//get the latest alphbat or digit
            tail--;
        if( !cmp(*head,*tail) && head<= tail)
        {
            return false;
        }
        else
        {
            head++;
            tail--;
        }
    }
    return true;
}

```

1.這題只要考慮  字母  與數字  其他符號可忽略不考慮

    所以必須分別寫出 isAlphbat & isDigit
    
    把字母跟數字混著一起考慮  會讓狀況更亂
    
2.分別用兩個指標  指向head & tail 

    1. 如果兩個Character 是字母
            則忽略大小寫  並判別是否想相同
    
    2. 如果兩個Character 是數字
          判別是否相同

3.終止條件就是tail>head囉

測資:
     char *ss="a.";  //true
     char *sss="aA"; //true
     char *ssss="0P"; //false


4.

看到有人這樣寫  用if + continue  其實這樣比較好   我原本寫的多個while 很容易讓人誤會

```c
while(head<tail)
{
    //while(!isAlphbat(*head) && !isDigit(*head))//get the first alphbat or digit
    //    head++;
    if(!isAlphbat(*head) && !isDigit(*head))//get the first alphbat or digit
        head++;
        continue;
        
    //while(!isAlphbat(*tail) && !isDigit(*tail))//get the latest alphbat or digit
    //    tail--;
    if(!isAlphbat(*tail) && !isDigit(*tail))//get the latest alphbat or digit
        head--;
        continue;
}
```

