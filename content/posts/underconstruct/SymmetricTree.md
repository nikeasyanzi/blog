
# [# 5.Binary Tree](/binaryTree.md)

# 101. Symmetric Tree
https://leetcode.com/problems/symmetric-tree/description/

    
        Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
        
        For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
        
            1
           / \
          2   2
         / \ / \
        3  4 4  3
        But the following [1,2,2,null,3,null,3] is not:
            1
           / \
          2   2
           \   \
           3    3
        Note:
        Bonus points if you could solve it both recursively and iteratively.
        

```c
bool isSym(struct TreeNode* left,struct TreeNode * right){
    if (left==NULL&&right!=NULL) return false;
    if (right==NULL&&left!=NULL) return false;
    if (left==NULL&&right==NULL) return true;
    if (left->val!=right->val) return false;
    
    if (!isSym(left->left,right->right)) return false; 
    if (!isSym(left->right,right->left)) return false;
    
    return true;
    
}

bool isSymmetric(struct TreeNode* root) {
    if(root==NULL){
        return true;
    }
    return isSym(root->left,root->right);
}
```


 https://leetcode.com/submissions/detail/153507685/



說明:

1. iterative 的話 應該用queue 但還沒時間做


Reference:

fisherlei.blogspot.tw/2013/01/leetcode-symmetric-tree.html   內有loop 版


