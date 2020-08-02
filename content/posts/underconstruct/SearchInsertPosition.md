# [Binary Search](/binarysearch.md)

## 35. Search Insert Position
https://leetcode.com/problems/search-insert-position/description/


https://leetcode.com/submissions/detail/143203586/
https://leetcode.com/submissions/detail/143202966/

### while loop版
```c

int bisearchloop(int *nums,int leftidx,int rightidx, int key) {
    int mid;
    int result=-1; //result idx
    int left=leftidx;
    int right=rightidx;
    while(1) {
        if(left<=right) {
            mid=right-left/2 + left;
            if(nums[mid]==key) {
                result=mid;
                break;
            }
            else {
                if(nums[mid]<key) {
                    left=mid+1;
                } else {
                    right=mid-1;
                }
            }
        }
        else {
            result=right+1;
            break;
        }
    }
    return result; 
}                                                                                                                                                                                                     
```
####  遞迴版

```c
int bisearch(int *nums,int left,int right, int key) {

    int mid;
    
    if(left<=right) {
        mid=right-left/2 + left;
        if(nums[mid]==key) return mid;
        else {
    
            if(nums[mid]<key) return bisearch(nums,mid+1,right,key);
            else return bisearch(nums,left,mid-1,key);
        }
    }
    return right+1;
}


```



Q.為什麼 回傳right +1 就會是原本應該要被Insert的位子?

回傳right+1的時候 是left>right 代表這時候是mid > key (key 要放在右邊)
        
    例如 對5 elements 做binary search
    
    1st iteration:
    left=0, right=3, mid=2
    A[mid]<key -> bisearch(A,3,4,key)
    A[mid]>key -> bisearch(A,0,1,key)
    2st iteration:bisearch(A,3,4,key)
    mid=3
    A[mid]>key -> bisearch(A,3,2,key)//key 在mid 右邊但超出範圍 所以為原本mid的位置(right+1)
    A[mid]<key -> bisearch(A,4,4,key)
    3st iteration:bisearch(A,0,1,key)
    mid=1
    A[mid]>key -> bisearch(A,0,0,key)
    A[mid]<key -> bisearch(A,2,1,key) //key在mid左邊但已經超出界線 所以為right+1

考慮三種狀況
1.假設 key 是最小的,剛好符合mid>key的狀況
2.假設 key 是最大的,因為程式最後會檢查最右邊的數 但mid+1 又導致了left>right的狀況
所以回傳right+1沒錯
3.假設key 在陣列的某區間,因為是mid +1 or -1 最後都終止在left>right的狀況
也就是說right是我們要考慮的位子 但right 已經-1了




        

