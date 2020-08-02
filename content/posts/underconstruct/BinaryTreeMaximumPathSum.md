
# 124. Binary Tree Maximum Path Sum


https://leetcode.com/problems/binary-tree-maximum-path-sum/description/


    Given a binary tree, find the maximum path sum.
    
    For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.
    
    For example:
    Given the below binary tree,
    
           1
          / \
         2   3
    Return 6.

```c
int maxPath(struct treeNode *root, int *max)
{
    inline MAX( int a, int  b)  { return (a)>(b)?(a):(b);}
    if(root==NULL )
    {
        return 0;
    }
    int left;
    int right;
    left=MAX(maxPath(root->left,max),0);
    right=MAX(maxPath(root->right,max),0);

    if ( *max<left+right+root->val)
    {
       *max=left+right+root->val;
    }
    //printf("max=%d ,left=%d,right=%d\n",*max,left,right);
    return left>right?left+root->val:right+root->val;
}

int maxPathSum(struct TreeNode* root) {
    int max=INT_MIN;    // for the negative value test case
    maxPath(root,&max);
    return max;
}
```
策略:

考慮兩個狀態
single path:  1 -> 2  or 1->3
full path: 1->2->3 

所以對任一node 而言  計算該node 以下左右子樹的max path sum
    
重點:

1. 因為node有負數,max 要從INT_MIN 開始, 這樣即使max path sum 為負, 也會取代INT_MIN

2. 為何回傳left & right 的max path sum 為何要跟0比? 但跟INT_MIN 比 反而有錯??   // [2,-1] 會錯
因為這樣排除了left/right subtree 為負的狀態  接下來的if ( *max<left+right+root->val) 就會變成分別比較  left+root  right + root or root的狀態

3.利用一個global max 當參數  

4.return 回傳左右子樹中比較大的

測資
[9,6,-3,null,null,-6,2,null,null,2,null,-6,-6,-6]
[2,-1,-2]
[-3]

Reference:
http://www.cnblogs.com/grandyang/p/4280120.html
http://blog.csdn.net/wzy_1988/article/details/25290907

