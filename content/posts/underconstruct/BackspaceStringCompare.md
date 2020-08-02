# [9.Stack](/stack.md)

## 844. Backspace String Compare

https://leetcode.com/contest/weekly-contest-87/problems/backspace-string-compare/


說明:

1. 就是做兩個stack 出來 分別處理  然後比較

2. pop 要注意
    
    1. head 會因為pop 完了而改變

    2. 注意要把prev ->next 改null  指標不要亂指!!

3. 用array做好像也可以   但每次idx 操作  都很容易出錯

```c
struct node {
    char val;
    struct node *next;
};
void showall(struct node *head){
    struct node *curr=head;

    while( curr!=NULL ){
        printf("%c", curr->val);
        curr=curr->next;
    }
    printf("\n");
}
char pop(struct node **head ){
    struct node *curr=*head;
    struct node *prev=NULL;
    char val;
    if(curr!=NULL){
        while(curr->next!=NULL ){
            prev=curr;
            curr=curr->next;
        }
        if(curr==*head) *head=NULL;
        if(prev!=NULL) prev->next=NULL;
        val=curr->val;
        free(curr);
    }
    return val;
}

void push(struct node **head, char val ){
    struct node *curr=*head;
    struct node *newnode=malloc(sizeof(struct node));
    newnode->val=val;
    newnode->next=NULL;
    
    if(*head==NULL){
        *head=newnode;    
    }
    else{
        while(curr->next!=NULL){
            curr=curr->next;
        }
        curr->next=newnode;   
    }
}
 bool isEmpty(struct node *head){
     if(head==NULL) return true;
     return false;
 }
 bool backspaceCompare(char* S, char* T) {
    struct node *headS=NULL;
    struct node *headT=NULL;
    int i=0;
    while(*(S+i)!='\0'){
        if(*(S+i)=='#') pop(&headS); 
        else{
            push(&headS,*(S+i));
        }
        i++;
    }
    i=0;
    while(*(T+i)!='\0'){
        if(*(T+i)=='#') pop(&headT); 
        else{
            push(&headT,*(T+i));
        }
        i++;
    }
    
    showall(headT);
        
    showall(headS);
    while(!isEmpty(headT) && !isEmpty(headS)){
        if(pop(&headT)!=pop(&headS)) return false;
    }
    if(!isEmpty(headT) || !isEmpty(headS)){
        return false;
    }
    return true;  
}

```