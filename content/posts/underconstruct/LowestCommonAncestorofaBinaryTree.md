
# [# 5.Binary Tree](/binaryTree.md)

## 236. Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/

    Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.
    
    According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”
    
    Given the following binary search tree:  root = [3,5,1,6,2,0,8,null,null,7,4]
    
            _______3______
           /              \
        ___5__          ___1__
       /      \        /      \
       6      _2       0       8
             /  \
             7   4
    Example 1:
    
    Input: root, p = 5, q = 1
    Output: 3
    Explanation: The LCA of of nodes 5 and 1 is 3.
    Example 2:
    
    Input: root, p = 5, q = 4
    Output: 5
    Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself
                 according to the LCA definition.
    
    



https://leetcode.com/submissions/detail/155836070/
    
```c

struct TreeNode* recursive(struct TreeNode* root, struct TreeNode* p, struct TreeNode* q){
    struct TreeNode* left;
    struct TreeNode* right;
    if(root==NULL) return NULL;
    
    if(root==p|| root==q) return root; //strange!!, it not pass if we check with the val  not the address
    
    left= recursive(root->left,p,q);
    right= recursive(root->right,p,q);
    
    if(left!=NULL && right !=NULL) return root;
    
    return (left!=NULL)?left:right;

}

struct TreeNode* lowestCommonAncestor(struct TreeNode* root, struct TreeNode* p, struct TreeNode* q) {
    return recursive(root, p,q);
}


```
說明:

1. 這題其實 可以用 tree traverse 紀錄遍訪的節點 於陣列中
最後比較 common 的部分

2.但這邊我們用recursive的方法
    
    1. 假設有找到  就回傳root

    2. 否則分別往左邊跟右邊找

    3. 如果回傳的部分
        
        1.left & right都有值  表示目前即為root
        
        2.若只有left有值  則回傳left  
        
        3.若只有right 有值  則回傳right
        

    4.最後一個卡陰的地方是   如果單純比較value 是會fail
    只能比較address
    

