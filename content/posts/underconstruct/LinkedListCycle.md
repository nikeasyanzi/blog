# [4.Linked List](/LinkedList.md)

# 141. Linked List Cycle

https://leetcode.com/submissions/detail/155181105/


# 142. Linked List Cycle II

https://leetcode.com/submissions/detail/155357605/

```c
bool hasCycle(struct ListNode *head) {
    struct ListNode *tortise;
    struct ListNode *hare;
    
    tortise=head;
    hare=head;
    if(tortise==NULL || tortise->next==NULL ) return false;
    while( tortise!=NULL){
        if(tortise->next!=NULL)
        {
            tortise=tortise->next;
        }
        hare=hare->next;

            tortise=tortise->next;
            if(tortise==hare) return true;
        
        
        
    }
    return false;
}
```


## Tortoise and Hare
```c
List * loopDetection(List *root){
List *hare=root;
List *tortoise=root;

	while(1){	//loop check
	if(hare==tortise) return true;
    	if(hare==NULL) return false;
    		hare=hare->next;
    	if(hare==NULL) return false;
    		hare=hare->next;
    		tortise=tortise->next;
    	if(hare==tortise) return true;
    }

	hare=root;//find loop entry point
	
	while(hare!=NULL){
		hare=hare->next;
		tortise=tortise->next;
		if(hare==tortise) break;	
	}
	return hare; 
}
```

這個find loop entry
必須在loop detection 完馬上找loop entry point

原理是
hare 回到原點
tortoise 留在原地
兩者一次動一格
再次相遇  即為 loop entry point

loop detection
http://codingfreak.blogspot.com/2012/09/detecting-loop-in-singly-linked-list_22.html

find loop entry
http://codingfreak.blogspot.com/2012/12/detecting-first-node-in-a-loop.html


1,cycle detection 重點在交錯式
要tortise 走一步hare 檢查是不是到終點
再走第二部
這是因為考慮   沒有cycle的狀況下

2. 邊界條件就是 list is empty 直接return false  (no cycle)

