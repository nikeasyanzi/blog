# [3. Array/String](/arraystring.md)

## 160. Intersection of Two Linked Lists


```c
struct ListNode *getIntersectionNode(struct ListNode *headA, struct ListNode *headB) {
    struct ListNode *ptrA=headA;
    struct ListNode *ptrB=headB;
    if(ptrA==NULL||ptrB==NULL) return NULL;
    while(ptrA!=ptrB){
        //(ptrA==ptrB) return ptrA;
        ptrA=ptrA->next;
        ptrB=ptrB->next;
        
        if(ptrA==NULL && ptrB==NULL) return NULL;

        if(ptrA==NULL)
        ptrA=headB;
        if(ptrB==NULL)
        ptrB=headA;
    }
    return ptrA;
}
```


基本原理是

假設
list A =  XXX + common
list B =  YY+ common

則  見圖示

list A + list B = XXX + common + YY + common
list B + list A = YY + common + XXX + common

所以如果最後有相交
會在最後common部分相遇



Reference:
https://blog.csdn.net/NoMasp/article/details/50572819