
# [8.Misc](/misc.md)

## 840. Magic Squares In Grid

    A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.
    
    Given an grid of integers, how many 3 x 3 "magic square" subgrids are there?  (Each subgrid is contiguous).
    
    Example 1:
    
    Input: [[4,3,8,4],
            [9,5,1,9],
            [2,7,6,2]]
    Output: 1
    Explanation: 
    The following subgrid is a 3 x 3 magic square:
    438
    951
    276
    
    while this one is not:
    384
    519
    762
    
    In total, there is only one magic square inside the given grid.
    Note:
    
    1 <= grid.length <= 10
    1 <= grid[0].length <= 10
    0 <= grid[i][j] <= 15
    

```c
int check( int * rol_result, int * col_result, int dia1, int dia2){
    for (int i=0; i<3;i++){
        //printf("rol_result[i]=%d,col_result[i]=%d\n",rol_result[i],col_result[i]);
        if(rol_result[i]!=rol_result[0]) return false;
    
        if(col_result[i]!=col_result[0]) return false;            
    }
    //printf("dia1=%d,dia2=%d\n",dia1,dia2);

    if(dia1!=dia2) return false;
    if(dia1!=col_result[0]) return false;
            
    return true;
}

int hash_check(int **grid, int row,int col){
    int i;
    int j;
    int hash[9]={0};

    for (i=0;i<3;i++){        
        for (j=0;j<3;j++){
             if( grid[row+i][col+j]>9 || grid[row+i][col+j]<1 ) return false;
             
             if(hash[grid[row+i][col+j]-1]==0){   
                hash[grid[row+i][col+j]-1]=1;
             }else{
                    return false;      
             }
             printf("*(grid* i*rowsize+j)=%d\n",grid[row+i][col+j]);
        }
    }
    return true;
    
}

int numMagicSquaresInside(int** grid, int gridRowSize, int *gridColSizes) {

    int count=0;
    int k;
    int j;
    if (gridRowSize <3 || *gridColSizes<3) return false;
    int col_result[3];
    int row_result[3];
    int i;
    int dia1;
    int dia2;
    printf("gridRowSize=%d, *gridColSizes=%d\n",gridRowSize, *gridColSizes);
    int tmp;

    for (i=0;i<(*gridColSizes)-2;i++){
        
        for (j=0;j<gridRowSize-2;j++){
            printf("i=%d,j=%d\n",i,j);
            if(hash_check(grid,j,i)==false) continue;
                        
            for (k=0;k<3;k++){
                printf("grid[j][i] =%d\n",grid[j+k][i]);
                printf("grid[j][i+1] =%d\n",grid[j+k][i+1]);
                printf("grid[j][i+2] =%d\n",grid[j+k][i+2]);

                row_result[k]=grid[j+k][i] + grid[j+k][i+1] + grid[j+k][i+2];   

                printf("grid[j][i] =%d\n",grid[j][i+k]);
                printf("grid[j+1][i] =%d\n",grid[j+1][i+k]);
                printf("grid[j+2][i] =%d\n",grid[j+2][i+k]);
                
                col_result[k]=grid[j][i+k] + grid[j+1][i+k] + grid[j+2][i+k];          
                printf("=====\n");
            }
            dia1=grid[j][i]+grid[j+1][i+1]+grid[j+2][i+2];
            dia2=grid[j][i+2]+grid[j+1][i+1]+grid[j+2][i];
         
            printf("check=%d\n",check(row_result,col_result,dia1,dia2));
            if(check(row_result,col_result,dia1,dia2)==1) count ++;
        }
    }
    return count;
}
```

說明:
這題浪費很多時間 實在不應該

| (0,0) | (0,1) | (0,2) | (0,3) |
| ------------- |-------------| -----|----------|
| (1,0) |(1,1) |(1,2) | (1,3) |
| (2,0) |(2,1) |(2,2) | (2,3) |
| (3,0) |(3,1) |(3,2) | (3,3) |
| (4,0) |(4,1) |(4,2) | (4,3) |



1. sliding windows 的方式可以 是

    1. 從 i=0, j=0 當中心點
    計算的範圍就是0~ row-3 & 0 ~ col-3      
    2. 從 i=1,j=1開始 當中心點
    就計算 i-1 ~ row -2 & j-2 ~ col -2

2. sliding windows 無法加速  因為這樣讓程式複雜很多

3. 最後直接硬幹  檢查 
sum of each row
sum of each col
sum of diag
each number 1~9 appear once

