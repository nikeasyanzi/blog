

#110. Balanced Binary Tree
    
    Given a binary tree, determine if it is height-balanced.
    
    For this problem, a height-balanced binary tree is defined as:
    
    a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
    
    Example 1:
    
    Given the following tree [3,9,20,null,null,15,7]:
    
        3
       / \
      9  20
        /  \
       15   7
    Return true.
    
    Example 2:
    
    Given the following tree [1,2,2,3,3,null,null,4,4]:
    
           1
          / \
         2   2
        / \
       3   3
      / \
     4   4
    Return false.

```c
    #include <math.h>
    #define MAX(a,b) (a)>(b)?(a):(b)
    #define MIN(a,b) (a)<(b)?(a):(b)
    #define ABS(a,b) ((a)>(b))?((a)-(b)):((b)-(a)) //wrong
    #define abss(x)  ( ( (x) < 0) ? -(x) : (x) )
    
    int getDepth(struct TreeNode *N, int *result)
    {
        int left=0;
        int right=0;
        
        if (N == NULL)
            return 0;
        left=getDepth(N->left,result);
        right=getDepth(N->right,result);
         if( abss(left-right)>1 && *result==true)
        {   
            printf("MAX(left,right)-MIN(left,right) )= %d, %d, left=%d, right=%d, val=%d\n"\
            ,ABS(left,right), abss(left-right),left,right,N->val);
            *result=false;
        }
        return left>right?+left+1:right+1;
    }
    int balanceCheck(struct TreeNode* root){
        int result=true;
        getDepth(root,&result);
        return result;
    }
    
    bool isBalanced(struct TreeNode* root) {
        return balanceCheck(root); 
    }
```

這題 檢查是否為平衡數   定義為 左右子樹level不能大於1
基本上每個node recursive 檢查即可

遇到的問題:

if( ABS(left-right)>1 && *result==true)  ->判斷會錯誤

改成呼叫abss(left-right) 或者 math.h 裡面的abs()  都正常

後來才發現是要多加括號

改成 if( ( ABS(left-right) ) >1 && *result==true)  
或者 
Macro 改成
```c
#define ABS(a,b) (((a)>(b))?((a)-(b)):((b)-(a))) 
```
很明顯 Macro 很雷

