 [# 5.Binary Tree](/binaryTree.md)

# 98. Validate Binary Search Tree

    Given a binary tree, determine if it is a valid binary search tree (BST).
    
    Assume a BST is defined as follows:
    
    The left subtree of a node contains only nodes with keys less than the node's key.
    The right subtree of a node contains only nodes with keys greater than the node's key.
    Both the left and right subtrees must also be binary search trees.
    Example 1:
    
    Input:
        2
       / \
      1   3
    Output: true
    Example 2:
    
        5
       / \
      1   4
         / \
        3   6
    Output: false
    Explanation: The input is: [5,1,4,null,null,3,6]. The root node's value
                 is 5 but its right child's value is 4.
                 
https://leetcode.com/problems/validate-binary-search-tree/description/

```c
bool isBST(struct TreeNode * curr, struct TreeNode* left, struct TreeNode* right)
{
//printf("val=%d\n", curr->val);
// Base condition
    if (curr == NULL)
        return true;
// if left node exist that check it has
// correct data or not

    if (left != NULL && curr->val <= left->val)
        return false;

// if right node exist that check it has
// correct data or not
    if (right != NULL && curr->val >= right->val)
        return false;

// check recursively for every node.
    return isBST(curr->left, left, curr) &&
           isBST(curr->right, curr, right);
}

bool isValidBST(struct TreeNode* root)
{
    return isBST(root,NULL,NULL);
}
```

### Explanation

Thre problem is tricky, be careful with the conrer test cases such as 
\[1,1\] 
\[2,1,3,NULL,NULL,5\] 
[10,5,15,null,null,6,20]



          2                      1                        
       1      3                       1
            5
           
           
          10 
              
       5      15   
            
            6    20
           


所以基本上 只要直接確定 

1. if it is a null node, return true

2. check a node whether  left < node && node < right 
不能重複
3. check left sub tree and right sub tree

[https://leetcode.com/submissions/detail/140847741/](https://leetcode.com/submissions/detail/140847741/)


1.用中序既然是binary search tree, 
infix 應該是 monotenous increasing
算是最好的解  但耗費記憶體

2.範圍法  max and min
如果你想用限定範圍的方法  但會有致命錯誤
如           
Narrowing down the range between curr-&gt;key+1 ~ int\_MAX  and int\_MIN ~ curr-&gt;key+1 leads to a lethal bug, the program goes wrong when there are two INT\_MIN or INT\_MAX.
因為你用範圍法就表示 
node val不能為INT_MAX or INT_MIN

