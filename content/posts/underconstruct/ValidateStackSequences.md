#[9.Stack](/stack.md)


##[946. Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/)

```python
class Solution:
    def validateStackSequences(self, pushed, popped):
        """
        :type pushed: List[int]
        :type popped: List[int]
        :rtype: bool
        """
        mylist=[];
        if len(pushed)!=len(popped):
            return False;
        
        while popped != []:
            #print("pop=",popped,"pushed=",pushed,"mylist=",mylist);
            if pushed != [] and pushed[0]==popped[0]:
                pushed.pop(0);
                popped.pop(0);

            elif mylist != [] and mylist[-1]==popped[0]:
                mylist.pop(-1);
                popped.pop(0);

            elif pushed!=[]:
                mylist.append(pushed.pop(0));
            else:
                return False;
        return True;
```    

說明: 這題是要驗證stack 的output  基本上是straight forward

只要檢查mylist[-1] 或者 pushed[0] 是否為poped[0]即可

namely, loop over 每個 element in poped 
必找到一個對應的element 在mylist or pushed


Test case:    
Popped:[4, 3, 5, 1, 2]
Pushed:[1, 2, 3, 4, 5]

popped| pushed| mylist| 
---|:-----:|
[4, 3, 5, 1, 2]|[1, 2, 3, 4, 5] |[]|
[4, 3, 5, 1, 2] |[2, 3, 4, 5]|[1]
[4, 3, 5, 1, 2]|[3, 4, 5] | [1, 2]
[4, 3, 5, 1, 2]|[4, 5] |[1, 2, 3]
[3, 5, 1, 2] | [5] |[1, 2, 3]
[5, 1, 2] | [5] | [1, 2]
[1, 2]| [] | [1, 2]


Popped:[4, 3, 5, 1, 2]
Pushed:[1, 2, 3, 4, 5]

Popped| Pushed| mylist| 
---|:-----:|
[4, 5, 3, 2, 1] | [1, 2, 3, 4, 5] |[]
[4, 5, 3, 2, 1] | [2, 3, 4, 5] |[1]
[4, 5, 3, 2, 1] | [3, 4, 5]| [1, 2]
[4, 5, 3, 2, 1] | [4, 5] | [1, 2, 3]
[5, 3, 2, 1] | [5] | [1, 2, 3]
[3, 2, 1] | [] | [1, 2, 3]
[2, 1] | [] | [1, 2]
[1] | [] | [1]