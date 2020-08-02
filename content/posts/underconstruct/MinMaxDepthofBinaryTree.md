#[5.Binary Tree](/binaryTree.md)

### 104. Maximum Depth of Binary Tree

    Given a binary tree, find its maximum depth.
    
    The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
    
    Note: A leaf is a node with no children.
    
    Example:
    
    Given binary tree [3,9,20,null,null,15,7],
    
        3
       / \
      9  20
        /  \
       15   7
    return its depth = 3.



https://leetcode.com/problems/maximum-depth-of-binary-tree/




```c
int getDepth(struct TreeNode* curr, int depth, int final)
{
    if(curr == NULL)
    {
        if(depth > final)
        {
            final=depth;
        }
        return final;
    }
    depth++;

    final=getDepth(curr->left, depth,final);
    final=getDepth(curr->right,depth,final);
    printf("val=%d, depth=%d, final=%d\n",curr-&gt; val, depth,final);
    return final;
}

int maxDepth(struct TreeNode* root)
{
    int result;
    result=getDepth(root,0,0);
    return result;
}
```

This is A top down approach, the level is increased and passed down to the child node.

[https://leetcode.com/submissions/detail/140867659/](https://leetcode.com/submissions/detail/140867659/)

這是另一個解法   原理差不多 但這是bottom up的解法  意即   
返回上一層caller時才把depth+1

```c
int maxDepth(struct TreeNode* root)
{
    int maxright;
    int maxleft;
    if(root==NULL)
        return 0;
    maxright=maxDepth(root->right);
    maxleft=maxDepth(root->left);
    printf("%d  %d %d", root->val, maxright,maxleft);
    return (maxright>maxleft)?(maxright +1): (maxleft+1);
}
```

但這題非遞迴的話   其實要用BFS 來解






# 111. Minimum Depth of Binary Tree


    Given a binary tree, find its minimum depth.
    
    The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
    
    Note: A leaf is a node with no children.
    
    Example:
    
    Given binary tree [3,9,20,null,null,15,7],
    
        3
       / \
      9  20
        /  \
       15   7
    return its minimum depth = 2.

https://leetcode.com/problems/minimum-depth-of-binary-tree/description/

```c
int getDepth(struct TreeNode* curr]
{
int depth;
int left;
int right;
    if(curr==NULL){
    return 0;
    }

    if(curr!=NULL && curr->right ==NULL && curr->left==NULL){
        return 1;
    }
    if( curr->right !=NULL && curr->left!=NULL ){
        left=getDepth(curr->left);
        right=getDepth(curr->right);
        depth= left<right?left:right;
    }

    if( curr->right ==NULL && curr->left!=NULL){
        depth=getDepth(curr->left);
    }

    if( curr->right !=NULL && curr->left==NULL){
        depth=getDepth(curr->right);
    }
    return depth+1;
}

int minDepth(struct TreeNode* root){
    return getDepth(root);
}
```
https://leetcode.com/submissions/detail/140981427/


### Explanation

Minimum Depth of Binary Tree
[29 和Minimum depth of binary tree 的 概念很像

1. 計算深度的方法可以top down or bottom up

1. top-down: we consider the depth of root as 1, and gradually increase the depth when visiting the successors.

2. bottom-up: we consider the depth of leaf as 1 and gradually increase the depth when visiting the predecessors

2. 考慮node的狀態

1. null node

2. node with two child nodes

3. node with either right or left child node

3. The curr depth can be updated by consider the depth of left subtree and the depth of right subtree.

4. Maximum Depth of Binary Tree 和Minimum depth of binary tree 的差別

1](/questions/MinMaxDepthofBinaryTree. Max depth 從root node 計算起 較方便

2. Min depth 從leaf node算起比較方便

3. 比較一下兩者演算法,可以發現Minimum depth的算法須額外分辨只有左或右子樹的狀況, 否則只有空子樹的深度被回傳md)
