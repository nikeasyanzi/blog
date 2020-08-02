# [# 4.Linked List](/LinkedList.md)

# 203. Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements/description/


```c
struct ListNode* removeElements(struct ListNode* head, int val) {
    struct ListNode* curr=head;
    struct ListNode* prev=head;
    
    while(curr!=NULL){
        if(curr->val==val){//move to next
            if(curr==head){ //chech if the head element needs to be removed;
                head=head->next;
                free(prev);
                prev=head;
                curr=head;
            }else{
                //printf("curr->val=%d prev->val=%d\n",curr->val,prev->val );
                prev->next=curr->next;
                free(curr);
                curr=prev->next;// realigment curr    
            }
        }else{
            prev=curr;
            curr=curr->next;
        }
    }
    return head;
}
```


test case:
[1,2,2,1]
2

[6,2,6,3,4,5,6]
6

第一個test case 要注意是 連續兩次remove, curr 指向的問題

第二個test case 要注意是 頭尾的coner case
