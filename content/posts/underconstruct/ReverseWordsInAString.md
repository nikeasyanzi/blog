## [3. Array/String](/arraystring.md)

### Reverse words in a string


	Given an input string, reverse the string word by word.
	
	Example:  
	
	Input: "the sky is blue",
	Output: "blue is sky the".


超機車這題


"abc def" -> "def abc"

步驟分成

1. 空白要處理
    
    1. 移除spaces at tail

    2. 移除spaces at head

    3. 保留一個space in the text and remove the rest

2. 先反轉每個單字

3. 接著頭尾交換


例子 " abc def "
->
處理空白:"abc def"
->
反轉單字:"cba fed"
->
每個頭尾字元交換:"def abc"

```c
int removeSpace(char *s, int i)
{
	int spaceCount;
	int k;
	int j;
	spaceCount=1;
	while(s[i+spaceCount]==' ')
	{
		spaceCount++;
	}
	k=0;
	while(s[i+k+spaceCount]!='\0') //lets move forward
	{
		swap(s, i+k,i+k+spaceCount);
		k++;
	}
	s[i+k]='\0';
	j=i+k-1;
	return j;
}
void reverseWords(char *s)
{
	int len=0;
	int j;
	int i=0;
	int k=0;

	j=strlen(s)-1;
	printf("012345678901234567\n");
	printf("%s, len=%d, i=%d,j=%d\n\n",s,strlen(s),i,j);
	while(s[j]==32 & j>=0) //remove space at tail
	{
		s[j]='\0';
		j--;
	}
	if(s[0]==' ')
	{
		removeSpace(s,0); //remove head space
	}
	while(s[i]!='\0')
	{
		if(s[i]==' ' && s[i+1]== ' ') //
		{
			removeSpace(s,i+1); //remove middle space
		}
		i++;
	}
	printf("%s, len=%d, i=%d,j=%d\n\n",s,strlen(s),i,j);

	j=0;
	i=0;
	while( s[i]!='\0' )
	{
		i++;
		if (s[i] == '\0')
		{
			reverse(s,j, i-1);
		}
		else if(s[i] == ' ')
		{
			reverse(s,j, i-1);
			j = i+1;
		}
	}
	i=0;
	reverse(s,i,strlen(s)-1);
	printf("%s, len=%d, i=%d,j=%d\n\n",s,strlen(s),i,j);

}

https://leetcode.com/submissions/detail/147994217/


```
Reference:https://www.geeksforgeeks.org/reverse-words-in-a-given-string/



# 186 Reverse words in a string 2
這題鎖起來了  但這題更簡單   所以跳過
