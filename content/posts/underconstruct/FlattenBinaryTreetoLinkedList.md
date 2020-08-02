# [5.Binary Tree](/binaryTree.md)

## 114. Flatten Binary Tree to Linked List

https://leetcode.com/problems/flatten-binary-tree-to-linked-list/


             1                    1                    1                    1
           /   \     move 2        \         move 4     \                    \
          2     3    append 3       2        append 5    2       move 7       2
        /  \          ===>         /  \       ===>        \       ===>         \   
       4    5                     4    5                   4                    4
       \    /                     \   / \                   \                    \
        6  7                      6  7  3                    6                    6
                                                              \                    \
                                                               5                    5 
                                                              / \                    \
                                                             7   3                    7     
                                                                                       \
                                                                                        3   




```c
void insert(struct TreeNode* root,struct TreeNode* tmp){
    struct TreeNode* curr=root;
  
    while(curr->right!=NULL){
        curr=curr->right;
    }
    curr->right=tmp;
}

void flatten(struct TreeNode* root) {
    struct TreeNode* curr=root;
    struct TreeNode* tmp;
    
    while(curr!=NULL){
        if(curr->left!=NULL){
            tmp=curr->right;
            curr->right=curr->left;    // move the original right subtree to the left
            curr->left=NULL;
            insert(curr->right,tmp);   // move the descendants of the original right subtree to the right of the original left subtree
        }
            curr=curr->right;
    }
}
```

這題主要分成兩部分

1.move the left subtree to the right

2.move the descendants of the original right subtree to the right of the original left subtree
