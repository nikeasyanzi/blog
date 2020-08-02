# [4.Linked List](/LinkedList.md)

# 19. Remove Nth Node From End of List
https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/

```c
struct ListNode* removeNthFromEnd(struct ListNode* head, int n) {
    struct ListNode* prev = head;
    struct ListNode* curr = head;
    struct ListNode* tmp;
  
    int i=0;
    for(i=0;i<n;i++) curr=curr->next;
    if(curr==NULL) {        // remove the head one
        tmp=head;
        head=head->next;
        return head;
    }       
    while(curr->next!=NULL){
        curr=curr->next;
        prev=prev->next;
    }
    tmp=prev->next;
    free(tmp);
    prev->next=prev->next->next;
    return head;
}
```


很巧妙的一題  
一個loop 解完全部 
有夠厲害


假設一個長度為5的 list

case1. remove N=2 
    curr 先移動到n=2的位置
    接著 prev 與curr 分別移動3個位置 
    
    所以 prev 指向3的位置  curr指向最後一個
    
    這時你會發現  prev 指的位置 剛好就是  我們要處理的地方
    
case2. remove N=3
    同理可得  N=3也成立 
