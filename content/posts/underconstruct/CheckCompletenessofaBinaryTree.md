# [5.Binary Tree](/binaryTree.md)

# 958. Check Completeness of a Binary Tree

https://leetcode.com/contest/weekly-contest-115/problems/check-completeness-of-a-binary-tree/

Input: [1,2,3,4,5,6]
Output: true

        1
      2   3
     4 5 6


Input: [1,2,3,4,5,null,7]
Output: false

        1
      2   3
    4  5   7


Input: [1,2,3,4,5,6,null,8,9]
Output: false

            1
         2     3
       4   5  6
      8 9
    

```python
class Solution:
    def isCompleteTree(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.helper([root]);
        
    def helper( self, myqueue):
        while myqueue!=[]:
            #print(myqueue);
            node=myqueue.pop(0);
            #print(node.val);
            if node==None:
                while myqueue!=[]:    # check if the residual nodes are null or not.
                    node=myqueue.pop(0);
                    if node!=None:
                        return False;
                return True;

            else:
                #print("append ",node.left.val," and ",node.right.val);
                myqueue.append(node.left);
                myqueue.append(node.right);
  
 ```
 
 說明:
 1. 這題是檢查是否為complete tree , 條件就是如果node 為null, 則 之後的node 也必須為node
 
 2. 用BFS 做檢查就好