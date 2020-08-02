# [5.Binary Tree](/binaryTree.md)

## 866. Smallest Subtree with all the Deepest Nodes
https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes/description/


Given a binary tree rooted at root, the depth of each node is the shortest distance to the root.

A node is deepest if it has the largest depth possible among any node in the entire tree.

The subtree of a node is that node, plus the set of all descendants of that node.

Return the node with the largest depth such that it contains all the deepest nodes in it's subtree.

Example 1:

Input: [3,5,1,6,2,0,8,null,null,7,4]
Output: [2,7,4]
Explanation:

                3
              /   \
           5        1
          / \      /  \
        6    2    0    8
            /  \
           7    4

We return the node with value 2, colored in yellow in the diagram.
The nodes colored in blue are the deepest nodes of the tree.
The input "[3, 5, 1, 6, 2, 0, 8, null, null, 7, 4]" is a serialization of the given tree.
The output "[2, 7, 4]" is a serialization of the subtree rooted at the node with value 2.
Both the input and output have TreeNode type.



解題心得

1.基本上 deepest node 一定是
left = null, right =null 

2.若level of right =level of left

return current

3. 
level of right !=level of left 
return level 低的那個



```python
class Solution:
    def subtreeWithAllDeepest(self, root):
        if root != None :
            level,ans=self.recursive (root,0);

            return ans;
        else:
            return None;
        
    def recursive(self, curr,level):
        rightlevel=0;
        leftlevel=0;
        if curr.left==None and curr.right==None:
            return level,curr;

        if curr.left!=None:
           leftlevel,left =self.recursive(curr.left,level+1);

        if curr.right!=None:
            rightlevel,right= self.recursive(curr.right,level+1);

        #print("leftlevel=",leftlevel,"rightlevel=",rightlevel);
        if leftlevel==rightlevel:
            return leftlevel,curr;
        else:
            if leftlevel>rightlevel:
                return leftlevel,left;
            else:
                return rightlevel,right;

```

Reference:
https://www.youtube.com/watch?v=A-8ziQc_4pk
