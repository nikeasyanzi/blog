# [5.Binary Tree](/binaryTree.md)

[100. Same Tree](https://leetcode.com/problems/same-tree/description/)

很簡單這題

```python

bool recursive(struct TreeNode* p, struct TreeNode* q){
    int left;
    int right;
    if (p ==NULL && q ==NULL) return true;
    if ( p ==NULL && q!=NULL) return false;
    if ( p !=NULL && q==NULL) return false;
    
    right= recursive(p->right,q->right) ;
    left= recursive(p->left,q->left);

    if ((left == false )||  ( right == false ) || (p->val !=q->val)){
        return false;
    }
    else{
        return true;
    }

}

bool isSameTree(struct TreeNode* p, struct TreeNode* q) {
    
    return recursive(p,q);
    
}
```


