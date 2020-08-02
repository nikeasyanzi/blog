


# 27. Remove Element
https://leetcode.com/problems/remove-element/description/
```python
class Solution:
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        head=0;  # looking for the nums[i]==2
        tail=len(nums)-1; # looking for the nums[i]!=2 
        if len(nums)==0:
            return 0;
        
        while(head<tail):
            if  nums[head]==val:
                while tail>head and nums[tail]==val:
                    tail=tail-1;
                print("head=",head," tail=",tail);
                if head==tail:
                    head=head-1;
                    break;
                nums[head]=nums[tail];
                nums[tail]=val;
                #tail--;    
            head=head+1;
        #print(head);
        return head+1;
```

# 203. Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements/description/

# 237. Delete Node in a Linked List
https://leetcode.com/problems/delete-node-in-a-linked-list/description/

