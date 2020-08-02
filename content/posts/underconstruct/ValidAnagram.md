# [3. Array/String](/arraystring.md)

# 242. Valid Anagram


https://leetcode.com/problems/valid-anagram/description/

想法很簡單
1.建立hashtable 來記錄元素出現的次數   剛好這題只會有lower case
2.如果是anagram  最後hashtable 每個元素都會是0

```c

bool isAnagram(char* s, char* t) {
    int hash[26]={0};
    int i=0;
    while (*(s+i)!='\0'){
        hash[*(s+i)-'a']++;
        i++;
    }
    i=0;
    while (*(t+i)!='\0'){
        hash[*(t+i)-'a']--;
        i++;
    }
    
    for(i=0;i<26;i++){
        if(hash[i]!=0) return false;
    }
    return true;
}
```


