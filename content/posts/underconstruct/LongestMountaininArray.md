# [3. Array/String](/arraystring.md)

845. Longest Mountain in Array
https://leetcode.com/problems/longest-mountain-in-array/description/


https://leetcode.com/submissions/detail/157178104/

解法很直覺

1.先找 遞增數列 
  這邊我是和周圍兩個元素比較   但其實應該跟前一個比較即可
2.再找遞減數列
  承1. 應該也是跟後一個比較即可
  
3.這邊要注意一下
山腳的idx(right=right+1)  因為decrease 是和後一個比  所以right +1 也是mountain的範圍

3.兩個都有找到
再用left & right做長度檢查


```c
int longestMountain(int* A, int ASize) {
    
    int i=0;
    int left=0;
    int right=0;
    int max=0;
    int len=0;
    bool increase=false;
    bool decrease=false;
    for(i=0;i<ASize-1;i++){ //find the increasing array
        left=i;
        while(i+1<ASize-1 && A[i]<A[i+1]){
            i++;
            increase=true;
        }
        
        //printf("left=%d i=%d ",left, i);
            if(left!=i){ //find the decreasing array
                while( i+1<ASize && A[i+1]<A[i]){
               // printf("a[%d]=%d \n",i,A[i]);

                right=i+1;  //here is the key point, 
                i++;
                decrease=true;
               // printf("a[%d]=%d,a[%d+1]=%d \n",i,A[i], i,A[i+1]);

            }    
        }
                
        //printf("right=%d ",right);

        if(increase&&decrease){
            len=right-left+1;
            i=right-1; 
            //printf("len=%d,",len);
        } 
        else{
            i=left;    // here is another keypoint, move the i to left
        }
        
        //printf("left=%d,right=%d,i=%d, increase=%d,decrease=%d\n", left, right,i,increase,decrease);
        
        increase=false;
        decrease=false;
        
        max=max>len?max:len;
        len=0;
    }
    return max;
    
}

```

