 [# 6.Binary Search](/binarysearch.md)

 
#[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

```c
int bisearch(int *a,int l,int r,int key){
    printf("left=%d,right=%d\n",l,r); 
    int mid;
    if(l<r){
        mid=(r-l)/2+l;
        if(a[mid]==key){
            
          return mid;
          
        }else{
          if(a[mid]<key) return bisearch(a,mid+1,r,key);
            else return bisearch(a,l,mid-1,key);       
        }
    }
    
    if(l==r){
      printf("left=%d,right=%d\n",l,r); 
      if(a[l]==key) return l;
    } 
    return -1;
}

int search(int* nums, int numsSize, int target) {
    int left=0;
    int right=numsSize-1;
    while(nums[left]>target) left++;
    while(nums[right]<target) right--;
    return bisearch(nums,left,right,target);
    
}
```

https://leetcode.com/submissions/detail/150060154/


有個特性要清楚
for any key in between the series 必定可以往左移或往右移
but for any key not in the series, it becomes loop over

ex. 4 5 6 7 0 1 2 3
key=6 search sequence is 4 5 6 7
key=2 search sequence is 0 1 2 3



#[81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

https://leetcode.com/submissions/detail/150063970/
```c
bool bisearch(int *a,int l,int r,int key){
    int mid;

    if(l<r){
        while(a[l]==a[r] && l!=r) r--; //remove the duplicate elements

        while(a[l]>key ){    // move to right
            l++;
            if(l==r) break;
        }
        while(a[r]<key) {    //move to left
            r--;
            if(l==r) break;
        }
        
        mid=(r-l)/2+l;

        if(a[mid]==key){
            return true;
        }else{
            if(a[mid]<key) return bisearch(a,mid+1,r,key);
            else return bisearch(a,l,mid-1,key);
        }
    }
    if(l==r){
        if(a[l]==key) return true;
    }
    return false;
}

bool search(int* nums, int numsSize, int target) {
    return bisearch(nums,0,numsSize-1,target);
}
```

作法跟上一題一樣

1.移除在頭尾的重複element
2.中間兩個while 迴圈 來保證數列變成是左小右大(中間可能還有其他重複)

ex. 4 4 6 7 1 3 3 3 4 4

-> 4 4 6 7 1 3 3 3

-> if key = 2

1 3 3 3

-> if key =5

4 4 6 7

if key = 0 變成單調搜尋
