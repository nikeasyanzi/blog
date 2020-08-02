# [9. Stack](/stack.md)

## 841. Keys and Rooms

    There are N rooms and you start in room 0.  Each room has a distinct number in 0, 1, 2, ..., N-1, and each room may have some keys to access the next room. 
    
    Formally, each room i has a list of keys rooms[i], and each key rooms[i][j] is an integer in [0, 1, ..., N-1] where N = rooms.length.  A key rooms[i][j] = v opens the room with number v.
    
    Initially, all the rooms start locked (except for room 0). 
    
    You can walk back and forth between rooms freely.
    
    Return true if and only if you can enter every room.
    
    Example 1:
    Input: [[1],[2],[3],[]]
    Output: true
        Explanation:  
        We start in room 0, and pick up key 1.
        We then go to room 1, and pick up key 2.
        We then go to room 2, and pick up key 3.
        We then go to room 3.  Since we were able to go to every room, we return true.
    
    Example 2:
    Input: [[1,3],[3,0,1],[2],[0]]
    Output: false
    Explanation: We can't enter the room with number 2.
    
    Note:
    1 <= rooms.length <= 1000
    0 <= rooms[i].length <= 1000
    The number of keys in all rooms combined is at most 3000.


```c
struct List {
    int val;
    struct List *next;    
};

struct List * push(struct List *head, int val){
    struct List *node=malloc(sizeof(struct List));
    struct List *curr = head;
    node->val=val;
    node->next=NULL;
    
    if(head==NULL){
        head=node;    
    }else{       
        while(curr->next!=NULL){
            curr=curr->next;
        }
        curr->next=node;
    }
    //printf("push=%d ",node->val);
    return head;
}

int pop(struct List **head){
    struct List *curr = *head;
    struct List *prev=curr ;

    int tmp;
    
    while(curr->next!=NULL){
        prev=curr;
        curr=curr->next;
    }
    prev->next=NULL;
    tmp=curr->val;
    //printf("pop=%d ",curr->val);

    if(curr==*head) *head=NULL;
        free (curr);
    return tmp;       
}

bool isEmpty(struct List *head){
    if (head!=NULL){
        return false;
    }
    return true;
}


void showall(struct List *head){
    struct List *curr = head;

    if(curr!=NULL) {   
        printf("showall %d ",curr->val);
        while(curr->next!=NULL){
            printf("%d ",curr->val);
            curr=curr->next;
        }
    }
    else{
        printf("showall = NULL ");
    }
}
bool canVisitAllRooms(int** rooms, int roomsRowSize, int *roomsColSizes) {
    struct List *head=NULL;
    int isVisited[3000]={0};
    int i=0;
    isVisited[0]=1;
    int val;
   // showall(head);
    for (i=0;i<roomsColSizes[0];i++){
        head=push(head,rooms[0][i]);
    } 
  // showall(head);
   
   while(!isEmpty(head)){
        //showall(head);
        if(!isEmpty(head)){
            
        val=pop(&head);
        //printf("isVisited[%d]=%d\n",val,isVisited[val]);
        if(isVisited[val]==0){
           isVisited[val]=1;
            //printf("roomsColSizes[val]=%d\n",val);
            //printf("head->val=%d\n",head->val);
           // showall(head);
            for (i=0;i<roomsColSizes[val];i++){
                //printf("rooms[val][i]=%d\n ",rooms[val][i]);
                head=push(head,rooms[val][i]);
            }    
             //showall(head);
        }
            
        }
    }
    
    for (i=0;i<3000;i++){
        roomsRowSize-=isVisited[i];   
    }
    
    if(roomsRowSize!=0) return false;
        
    return true;
}
```


說明:

1.就是用stack解  
此題可用DFS  or BFS 都可以

DFS 就用stack

BFS 就用queue

當然另外要一個hash tableisVisited 來記錄開過的房間

2. 如何檢查是否全部房間都開完

有個很技巧的檢查是不是所有房間都開完了
只要去計算hash table 開過的房間數 有沒有符合原本的roomsRowSize即可

測資
[[1,3],[3,0,1],[5],[0],[2]]  -> 2, 5 自成一圈
[[1,3],[3,0,1],[2],[0]] -> 2 自成一圈

心得: 
stack & queue 應該是心中要有模板

