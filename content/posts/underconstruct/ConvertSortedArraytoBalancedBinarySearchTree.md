# [# 5.Binary Tree](/binaryTree.md)
# 108. Convert Sorted Array to Binary Search Tree



https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/


![](https://i.imgur.com/4VfzfUn.png)



```c
    struct TreeNode* myinsertTree( int *nums, int left,int right)
    {
        struct TreeNode *newnode;
        if(left<=right)
        {
            newnode=malloc(sizeof(struct TreeNode));
            int midIdx=(right+left)/2;
            newnode->left=NULL;
            newnode->right=NULL;
            newnode->val=nums[midIdx];
            newnode->left=myinsertTree(nums, left,midIdx-1);
            newnode->right=myinsertTree(nums, midIdx+1,right);
            printf("%d ", newnode->val);
            return newnode;
        }
    return NULL;
}

    struct TreeNode* sortedArrayToBST(int* nums, int numsSize) {
    struct TreeNode *root=NULL;
    root=myinsertTree( nums, 0,numsSize-1);
    return root;
}

```


```c
    class Solution(object):
    def sortedArrayToBST(self, nums):
    """
    :type nums: List[int]
    :rtype: TreeNode
    """
    return self._sortedArrayToBST(nums, 0, len(nums))

    def _sortedArrayToBST(self, nums, left, right):
        if left == right:
            return None
        mid = (left + right) >> 1
        root = TreeNode(nums[mid])
        root.left = self._sortedArrayToBST(nums, left, mid)
        root.right = self._sortedArrayToBST(nums, mid + 1, right)
        return root

    if __name__ == "__main__":
        None
```

放這兩份code 表示

1.用於修改root的技巧 用回傳的

回傳下一層的newnode 給上層 的left/right 甚至是原本sortedArrayToBST()

2.
< = 的部分
一個是檢查 < =

一個是檢查 >

但 left>right 都會回傳null 表示子樹會被設成null

3.