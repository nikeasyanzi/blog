# [# 5.Binary Tree](/binaryTree.md)

## 112. Path Sum

https://leetcode.com/problems/path-sum/description/

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.

Example:

Given the below binary tree and sum = 22,

          5
         / \
        4   8
       /   / \
      11  13  4
     /  \      \
    7    2      1
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

```go
func recursive(root *TreeNode, sum int) bool{
    left := false  
    right := false  
    if root == nil {
        return false;
    }
    fmt.Printf("sum=%d root.Val=%d\n ",sum,root.Val);

    if root.Left==nil && root.Right==nil {
        if root.Val==sum {
            return true;
        }else{
            return false;
        }
    }else{
      if root.Left!=nil {
        left=recursive(root.Left,sum-root.Val)
      }  
      if root.Right!=nil { 
       right=recursive(root.Right,sum-root.Val)
      }          
    }
    return left || right
}
func hasPathSum(root *TreeNode, sum int) bool {
    return recursive(root,sum)
}

```
## 113. Path Sum II 
https://leetcode.com/problems/path-sum-ii/description/
用go 寫 感覺怪怪的  哭哭
卡在copy 很久      
slice append 預設是copy address 沒用copy 先重新複製一份出來  答案會是錯的
https://leetcode.com/submissions/detail/153651293/

```go

func recursive(root *TreeNode, sum int, current []int, final [][]int)  [][]int{
    //var tmp []int
    if root !=nil{
        current=append (current,root.Val)
        if root.Val==sum && root.Left==nil && root.Right==nil{
            tmp := make([]int, len(current))
            copy(tmp,current)
            //fmt.Println(tmp)
            //fmt.Println(current)
            final=append(final,tmp)
            return final
        }else{
            final=recursive(root.Left,sum-root.Val,current,final)
            final=recursive(root.Right,sum-root.Val,current,final)   
        } 
    }
    return final

}

func pathSum(root *TreeNode, sum int) [][]int {
    var current []int
    var final [][]int
    
    final=recursive(root,sum,current,final)
    
    return final 
}
```

## 437. Path Sum III

https://leetcode.com/problems/path-sum-iii/description/

```python
class Solution:
    def recursive(self,root,sum):
        left=0;
        right=0;
        count=0;
        if root==None:
            return 0;
        
        if sum==root.val:
            count=1;

        left=self.recursive(root.left,sum-root.val);
        right=self.recursive(root.right,sum-root.val);
            
        return count+left+right;
        
    
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: int
        """
        if root ==None:
            return 0;
        return self.recursive(root,sum)+self.pathSum(root.left,sum)+self.pathSum(root.right,sum);    
            
```

這題是 分成兩部分

1. 給你一個tree & sum
找從root 開始  累加  看有沒有符合sum

2. 這個tree 包含了subtree
所以從root 開始   
我們要遞迴的對每個subtree 找



