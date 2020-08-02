## [3. Array/String](/arraystring.md)


### 1. Two Sum
https://leetcode.com/problems/two-sum/description/

    Given an array of integers, return indices of the two numbers such that they add up to a specific target.
    
    You may assume that each input would have exactly one solution, and you may not use the same element twice.
    
    Example:
    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].
    

```c

int *result=NULL;
int *hash;
int* twoSum(int* nums, int numsSize, int target)
{
	int i;
	int min=INT_MAX;
	int max=INT_MIN;
	result=malloc(sizeof(int)*2);
	result[0]=-1;
	result[1]=-1;

	for (i=0; i<numsSize; i++) //get max and min to find the hash range
	{
		if(nums[i]<min) min=nums[i];
		if(nums[i]>max) max=nums[i];
	}
	if(target-min < min) min=target-min;
	if(target-max < min) min=target-max;
	if(target-min > max) max=target-min;
	if(target-max > max) max=target-max;
	hash=malloc(sizeof(int)*(max-min+1));
	for (i=0; i<max-min+1; i++)
	{
		hash[i]=-1;
	}

	for(i=0; i<numsSize; i++)
	{
		//printf("i=%d target-nums=%d\n",i,target-nums[i]);
		if( hash[nums[i]-min]!=-1 && i != hash[nums[i]-min])
		{
			result[0]=i;
			result[1]=hash[nums[i]-min];
			break;
		}else{
			hash[target-nums[i]-min]=i; //the ith element needs target-nums[i]
		}
	}
	return result;
}

```
```c++
class Solution {
	public:
		vector<int> twoSum(vector<int>& nums, int target) {
			vector <int> sol;
			map<int,int> myhash;
			map<int, int>::iterator iter;
			for(int i=0; i<nums.size(); i++)
			{
				iter = myhash.find(target-nums[i]);
				if(iter != myhash.end())
				{
					sol.push_back(iter->second);
					sol.push_back(i);
					return sol;
				}
				else
					myhash.insert(pair<int, int>(nums[i], i));
			}
			return sol;
		}
};
```

測資
int A[3]= {3,2,4}; //6

int B[2]= {3,3}; //6
int C[5]={-1,-2,-3,-4,-5}; //-8
int D[4]={-3,4,3,90}; //0
int E[4]={0,4,3,0};//0

## 這題解法

### 1.暴力法 兩個迴圈 O(N^2)

### 2.用hash table
也就是說

2.1假設n個數 其中的max & min 為hash table的大小

這個hash table 就很有學問
必須以一般的max & min作為hash table範圍

ex. target=30
最大數 max(n)=30
最小數 min(n)=-20
理論上hash 應該在-20 ~30
所以 hashtable為 max ~ min

2.2若對某數n , 紀錄hash [target-n ]是被需要的
1.紀錄該數n的index
hash[index] 這行不通
因為之後我們是用target-n 來檢查的
2.只能紀錄
hash[target-n]
3.考慮紀錄
hash[target-n]=0/1;
target-n 是否有被需要
表示target-n 有缺 但題目要回傳index 所以不行
	4.考慮紀錄index
hash[target-n]=某數n 的index (ok)
	target-n被n需要
	5.之後檢查 兩數的index 必不相同
	target=6 [3,4,0,3]
### hash table size 的決定

	要注意
	1.if(target-min < min) min=target-min;
	2.if(target-max < min) min=target-max;
	3.if(target-min > max) max=target-min;
	4.if(target-max > max) max=target-max;

	int E[4]={0,4,3,0};//0 ->最小是 0-4 =-4
找0 min= target-max

{-1,-2,-3,-8};

找-100 min=target-max
找0 max=target-min

{1,2,3,8};
找1 min=target -min


## 167. Two Sum II - Input array is sorted
https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution and you may not use the same element twice.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2


```c
int* twoSum(int* numbers, int numbersSize, int target, int* returnSize) {
	int left=0;
	int right=numbersSize-1;
	int val;
	int *result=NULL;
	result=(int *)malloc(sizeof(int)*2);
	result[0]=-1;
	result[1]=-1;
	while(left<right){
		val= numbers[left]+numbers[right];
		//printf("1left=%d, right=%d\n", left,right);

		if(val>target){         
			right--;
		}else{
			if(val<target) left++;
			else{
				result[0]=left+1;
				result[1]=right+1;
				*returnSize = 2;  
				//printf("2left=%d, right=%d\n", result[0], result[1]);
				break;
			}       
		}     
	}
	//printf("3left=%d, right=%d,size=%d\n", result[0], result[1],*returnSize);

	return result;
}
```

這個特性是
最小和是最右的兩個element
最大和是最左的兩個element

所以用夾的  

從最左 + 最右開始

1. > target 最右往右移

2. < target 最左往右移




