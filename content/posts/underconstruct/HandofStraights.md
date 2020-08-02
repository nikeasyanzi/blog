# [8.Misc](/misc.md)

# 846. Hand of Straights
https://leetcode.com/problems/hand-of-straights/description/

    Alice has a hand of cards, given as an array of integers.
    
    Now she wants to rearrange the cards into groups so that each group is size W, and consists of W consecutive cards.
    
    Return true if and only if she can.
    
     
    
    Example 1:
    
    Input: hand = [1,2,3,6,2,3,4,7,8], W = 3
    Output: true
    Explanation: Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8].
    Example 2:
    
    Input: hand = [1,2,3,4,5], W = 4
    Output: false
    Explanation: Alice's hand can't be rearranged into groups of 4.
    
作法:

    1.用hash table 計算每個value 出現的次數  
    
    2.由小到大   取 w 個元素成一個group
      
    3.這裡用了一個小技巧  一次取足
    
      假設hand=[1,2,2,3,4], w=3 
      這樣會出現[1,2,3] 但無法再組成[2,3,4]  
      所以事後再檢查  是否元素因此變負的(表示有不足的問題)
      
    4.全部減完 也要掃描一次  是否每個元素都歸0了
            
```python
class Solution:
    def isNStraightHand(self, hand, W):
        """
        :type hand: List[int]
        :type W: int
        :rtype: bool
        """
        dict = { };
        if(len(hand)%W!=0):
            return False;
        for i in range (len(hand)):
            if str(hand[i]) in dict:
                #print(dict[str(hand[i])])
                dict[str(hand[i])]=dict[str(hand[i])]+1;
            else:   
                dict[str(hand[i])]=1;
       
        dc_sort = sorted(dict.items(), key=lambda x:int(x[0]),reverse = False)
        #print(dc_sort)

        #print(len(dc_sort)-W)
        for i in range(len(dc_sort)-W+1):
            #print(i)
            #print(dc_sort)        

            if(dc_sort[i][1]!=0 ):
                for j in range (W-1):
                    if( i+j+1 > len(dc_sort) or int (dc_sort[i+j][0])+1 !=int (dc_sort[i+j+1][0]) ): 
                        return False;
                tmp=dc_sort[i][1];
                for j in range (W):
                        #print(j)
                        dc_sort[i+j]=list((str(dc_sort[i+j][0]),dc_sort[i+j][1]-tmp))
                        dc_sort[i]=list((str(dc_sort[i][0]),0))

                        if(int(dc_sort[i+j][1]) <0 ):# check if there is a insufficient problem
                            return False;
                        #print(dc_sort)        

            #print(dc_sort)     
        for i in range(len(dc_sort)):   //check if all become zero
             if(dc_sort[i][1]!=0 ):
                    return False;
        return True;
        
        
```