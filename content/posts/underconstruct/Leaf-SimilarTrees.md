
# [5.Binary Tree](/binaryTree.md)

[872. Leaf-Similar Trees](https://leetcode.com/contest/weekly-contest-94/problems/leaf-similar-trees/)


```python
class Solution:
    def recursive(self,root,result):
        if  root.left ==None and root.right==None:
            result.append(root.val);
            return;
        else:
            if root.left!=None:
                self.recursive(root.left,result);
            if root.right!=None:
                self.recursive(root.right,result);
        
            #return result;
        
    def leafSimilar(self, root1, root2):
        """
        :type root1: TreeNode
        :type root2: TreeNode
        :rtype: bool
        """
        result=[];
        self.recursive(root1,result);
        result2=[];
        self.recursive(root2,result2);
        
        for i in range (len(result2)):
            if result[i] != result2[i]:
                return False;
        return True;
        #print(result);
```


別人的作法

說穿了  就是一直找node   方便省事
```python
class Solution(object):
    def leafSimilar(self, root1, root2):
        """
        :type root1: TreeNode
        :type root2: TreeNode
        :rtype: bool
        """
        return self.findleaf(root1) == self.findleaf(root2)
        
    def findleaf(self, root):
        if not root: return []
        if not (root.left or root.right): return [root.val]
        return self.findleaf(root.left) + self.findleaf(root.right)
```
