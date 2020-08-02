# [3. Array/String](/arraystring.md)

# [900. RLE Iterator](https://leetcode.com/problems/rle-iterator/)

```python
class RLEIterator:
    def __init__(self, A):
        """
        :type A: List[int]
        """
        self.idx=0;
        self.A=A;
        
    def next(self, n):
        """
        :type n: int
        :rtype: int
        """
        #print("n=",n);
        #print("curr=",self.curr);
        tmp=0;
        while self.idx <=len(self.A)-2:   //loop over every 2 elements
            if n>0:        
                self.A[self.idx]=self.A[self.idx]-n;
            else:
                self.A[self.idx]=n+self.A[self.idx];
            #print ("n=",n,"self.A[self.idx]=",self.A[self.idx],"self.idx=",self.idx);

            if self.A[self.idx]<0:
                n=self.A[self.idx];    
                self.idx=self.idx+2;            
            else:
                #print ("return", self.A[self.idx+1]);
                return self.A[self.idx+1]; 
            
        #print ("return -1");
        return -1;
```

1. 這題不能傻傻展開 會TLE

2. 

example:
[[[3,8,0,9,2,5]],[6],[1],[1],[2]]
[[[3,8,0,9,2,5]],[2],[1],[1],[2]]


i| n| arr| 
--------------|-----|-----| 
-|-|[3,8,0,9,2,5]
0   | -3 |  [-3,8,0,9,2,5]
2    | -3 |  [-3,8,-3,9,2,5]
4  |-1 | [-3,8,-3,9,-1,5]  



