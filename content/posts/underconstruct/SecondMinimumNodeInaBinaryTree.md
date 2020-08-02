

# 671.  Second Minimum Node In a Binary Tree ()

https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/description/

    Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly two or zero sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes.
    
    Given such a binary tree, you need to output the second minimum value in the set made of all the nodes' value in the whole tree.
    
    If no such second minimum value exists, output -1 instead.
    
    Example 1:
    Input: 
        2
       / \
      2   5
         / \
        5   7
    
    Output: 5
    Explanation: The smallest value is 2, the second smallest value is 5.
    Example 2:
    Input: 
        2
       / \
      2   2
    
    Output: -1
    Explanation: The smallest value is 2, but there isn't any second smallest value.
    
    
    

```c
    void inorder(struct TreeNode*root, int *first,int *second){
    if(root->left!=NULL) inorder(root->left,first,second);
    printf("root->val=%d, first=%d,second=%d\n",root->val,*first,*second);
    if(root->val<*first){
        *second=*first;
        *first=root->val;
    }else{
        if(root->val>*first && root->val<*second){
        *second=root->val;
        }
    }
    if(root->right!=NULL) inorder(root->right,first,second);
}


int findSecondMinimumValue(struct TreeNode* root) {
    if (root==NULL ) return -1;
    int first=root->val;
    int second=INT_MAX;

    inorder(root,&first,&second);

    if(first==second || second==INT_MAX) return -1;
    
    return second;
}
```


**心得: 這種題目 is must get!**
But if the method is to do value comparsion, the element of tree node is equal to the limitation 
it  fails into a trap, that if a node val is (INT_MIN, INT_MAX)

