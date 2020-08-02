# [5.Binary Tree](/binaryTree.md)


#307. Range Sum Query - Mutable
https://leetcode.com/problems/range-sum-query-mutable/description/


```c
/**
* Your NumArray struct will be instantiated and called as such:
* struct NumArray* obj = numArrayCreate(nums, numsSize);
* numArrayUpdate(obj, i, val);
* int param_2 = numArraySumRange(obj, i, j);
* numArrayFree(obj);
*/
typedef struct {
    int *segementArr;
    int segementArrSize;
    int arrSize;
    int *arr;
} NumArray;
int construct(int arr[], int left, int right, int *st, int si){
    
     // If there is one element in array, store it in current node of
    // segment tree and return
    int mid = (right-left)/2 + left;
    
    //printf("mid=%d, ss=%d,se=%d\n",mid,ss,se);
    if (left == right)
    {
        st[si] = arr[left];
        return arr[left];
    }
 
    // If there are more than one elements, then recur for left and
    // right subtrees and store the sum of values in this node
    st[si] =  construct(arr, left, mid, st, si*2+1) +
              construct(arr, mid+1, right, st, si*2+2);
    return st[si];  
}
NumArray* numArrayCreate(int* nums, int numsSize) {
    NumArray *mySegArray=malloc(sizeof(NumArray));
    int i;
    int size;
    if (numsSize==0) return ; //input is empty
    //printf("numArrayCreate numsSize:%d\n",numsSize);

    //Height of segment tree
    int x = (int)(ceil(log2(numsSize))); 
 
    //Maximum size of segment tree
    int maxSize = 2*(int)pow(2, x) - 1; 
    mySegArray->arrSize=numsSize;
    mySegArray->segementArrSize=maxSize;
    mySegArray->arr=nums;
    mySegArray->segementArr=malloc(sizeof(int)* maxSize);
    construct( nums, 0, numsSize-1, mySegArray->segementArr, 0);
    
    //showall(mySegArray->segementArr,mySegArray->segementArrSize);
    return mySegArray;
}


void updateValue(NumArray * obj, int left, int right, int i, int diff, int idx)
{
    // Base Case: If the input index lies outside the range of 
    // this segment
    int j=0;
    int mid = (right-left)/2 + left;

    if (i < left || i > right)
        return;
    //showall(obj->segementArr,obj->segementArrSize);

    //printf("updateValue left=%d, right=%d, idx=%d, obj->segementArr[idx]=%d diff=%d,mid=%d\n",left,right,idx,obj->segementArr[idx],diff,mid);
    // If the input index is in range of this node, then update 
    // the value of the node and its children
    obj->segementArr[idx] =  obj->segementArr[idx] + diff;
    if (left != right)
    {
        updateValue(obj, left, mid, i, diff, 2*idx + 1);
        updateValue(obj, mid+1, right, i, diff, 2*idx + 2);
    }
}


void numArrayUpdate(NumArray* obj, int i, int val) {
    //printf("\nnumArrayUpdate: ");
    
    // Get the difference between new value and old value
    int diff = val -  obj->arr[i];

    // Update the value in array
    obj->arr[i] = val;
 
    // Update the values of nodes in segment tree
    updateValue(obj, 0, obj->arrSize-1, i, diff, 0);
    
    //printf("\nnumArrayUpdate: ");
    //showall(obj->segementArr,obj->segementArrSize);
}

int sumRange(NumArray* obj,int left,int right, int i, int j,int idx){
    int mid=(right-left)/2 +left;
    int left_val=0;
    int right_val=0;
    int k=0;
    //printf("mid=%d, left=%d,right=%d,i=%d,j=%d, j>left || right<i =%d,idx=%d \n",mid,left,right,i,j,(j>left || right<i),idx);
    
    if(i<=left && j>=right){
        return obj->segementArr[idx];
    }
    
    if(j<left || right<i){
        return 0;
    }
   
    //showall(obj->segementArr,obj->segementArrSize);

    return sumRange( obj, left, mid,  i,  j,2*idx+1) + sumRange(obj, mid+1, right,  i,  j,2*idx+2);
}
int numArraySumRange(NumArray* obj, int i, int j) {
    
    if(i<0 || j>obj->segementArrSize) return false;  // invalid range
    
    //printf("sumRange=%d ",sumRange(obj,0,obj->arrSize-1,i,j,0));

    return sumRange(obj,0,obj->arrSize-1,i,j,0);
}

void numArrayFree(NumArray* obj) {
    //printf("obj=%p,obj->segementArr=%p,",obj,obj->segementArr);
    //printf("recycling\n");
    //free(obj->segementArr);
    //free(obj);
    //printf("obj=%p,obj->segementArr=%",obj,obj->segementArr);
}
void showall(int *arr, int size){
    int k=0;
    for(k=0;k<size;k++){
      printf("%d ",arr[k]);
    }
     printf("\n");
}
```
Reference:

### A Recursive approach to Segment Trees, range sum queries & lazy propagation
https://leetcode.com/articles/a-recursive-approach-to-segment-trees-range-sum-queries-lazy-propagation/

Leetcode article: 307. Range Sum Query - Mutable 
https://leetcode.com/articles/range-sum-query-mutable/

Lazy Propagation in Segment Tree
https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/

Segment Tree | Set 2 (Range Minimum Query)
https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/
Segment Tree | Set 1 (Sum of given range)
https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/
