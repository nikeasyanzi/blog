#[5.Binary Tree](/binaryTree.md)

#653. Two Sum IV - Input is a BST

https://leetcode.com/problems/two-sum-iv-input-is-a-bst/

Similar questions: [TwoSum](/questions/TwoSum.md)
```c
class Solution:
    def findTarget(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: bool
        """
    def recursive(self,node,k,hashtable):
        #print(type(root.val));
        if node == None:
            return False;
        #print(node.val)
        #print(hashtable)
        #print((k - node.val) in hashtable)
        if node.val in hashtable:
            print(node.val)
            print(hashtable)
            return True;
        else:
            hashtable.append(k-node.val);
 
        return self.recursive(node.left,k,hashtable) or self.recursive(node.right,k,hashtable);   
    
    def findTarget(self, root, k):
        hashtable=[];
        return self.recursive(root, k,hashtable) ; 
    
```