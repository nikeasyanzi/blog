# 856. Score of Parentheses

https://leetcode.com/problems/score-of-parentheses/description/

    https://leetcode.com/problems/score-of-parentheses/description/
    
    Given a balanced parentheses string S, compute the score of the string based on the following rule:
    
    () has score 1
    AB has score A + B, where A and B are balanced parentheses strings.
    (A) has score 2 * A, where A is a balanced parentheses string.
    
    
    
```c
struct node{
    int val;
    struct node* next;
};

struct  node* push(struct node *head, int val){
    struct node *newNode=malloc( sizeof(struct node));

    newNode->val=val;
    newNode->next=NULL; // initialization

    struct node *curr=head;

    if (head==NULL) {
        head=newNode;
        head->next=NULL;
    }
    else {
        while(curr->next!=NULL){
            //printf("%d \n", curr->val);
            curr=curr->next;
        }
        curr->next=newNode;
    }
    return head;
}

int pop(struct node **head){
    struct node *curr=*head;
    struct node *prev;

    int val;
    while (curr->next!=NULL){
        prev=curr;
        curr=curr->next;
    }
    //printf("head=%p,curr=%p \n", *head,curr);

    if ((*head)==curr){
    *head=NULL;     //head may become null
        
    }else{
    prev->next=NULL;  // remember to clean the previous one
        
    } 
    val=curr->val;
    free(curr);
    return val;
}

int isEmpty(struct node *head){
    if(head!=NULL) return 0;
    return 1;
}

int showall(struct node *head){
    printf("showall:");
    struct node *curr=head;
    int val;
    while (curr!=NULL){
        printf("%d ",curr->val);
        curr=curr->next;
    }
    printf("\n");
    return 0;
}
int scoreOfParentheses(char* S) {

    int score=0;
    int val;
    struct node *head=NULL;
    int i=0;
    int tmp;
    while(*(S+i)!='\0'){
        switch(*(S+i)){
            case '(':
                head=push(head,-1);
                break;
            case ')':
                val=pop(&head);
                 if (val==-1){
                    head=push( head ,1);
                }
                else{
                        while(!isEmpty(head)){ // this is a key to handle the case  such as (()())  ->(1 1)->(2) -> 4
                            tmp=pop(&head);
                            if (tmp!=-1){
                                val=val+tmp;
                            }
                            else{
                                break;
                            }
                        }
                    val=val*2;
                    head=push(head,val);
                }
            break;
        }
        //showall(head);
        i++;
    }
    //showall(head); //now val in the stack is what we want
    while(!isEmpty(head)){ // this loop is to handle the case ()(),  the stack become 1 1 and final result is 2
        score=score+ pop(&head);
   }
    return score;
}
```

說明:
這種題目應該是老掉牙了  

不要過要注意

1. 一個新node 要初始化 
newNode->next=null

2. pop時 
注意head可能因此變null
另外prev->next 也要清空
 
這幾個該注意的地方 有註解

test case:
()
()()  //處理括號後 stack內會全是數字

(()())  // 要有兩倍的問題



