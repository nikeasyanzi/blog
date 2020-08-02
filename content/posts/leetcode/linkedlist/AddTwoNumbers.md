---
title:       "用 Hugo 建立部落格 / 網站，每步都有詳細教學"
subtitle:    "Wordpress、Blogger 以外的第三方案，設計彈性更高，並且免費，適合願意學寫程式的人。"
description: "自從去年學了程式，並開始工作以後，就有想建立部落格，寫下工程師日常的想法。在看了多數人推薦的 Wordpress 與 Google 的 Blogger 後，有了一些比較......"
date:         2019-04-19
author:      "Siddharam"
cover:       ""
image:       ""
tags:        ["教學", "Hugo", "部落格"]
categories:  ["技術筆記" ]
keywords:
- 教學
- Hugo
- 部落格
draft: false
---

disqusShortname : 'jiarongyang'



2. Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

    Example
    
    Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
    Output: 7 -> 0 -> 8
    Explanation: 342 + 465 = 807.
    

https://leetcode.com/problems/add-two-numbers/description/

```c

struct ListNode* head=NULL;
int showall(){
    struct ListNode* curr=head;
	while(curr->next!=NULL){
        printf("%d ", curr->val);
		curr=curr->next;
	}
    printf("\n======\n");
    return 0;
}

int addNode(int val1,int val2, int carryin)
{
    struct ListNode* curr=head;
    struct ListNode* newnode=malloc(sizeof(struct ListNode));
    newnode->next=NULL;
    int carryout=0;
    if(val1+val2+carryin<10)
    {
        newnode->val=val1+val2+carryin;
        carryout=0;
    }
    else
    {
        //printf(" in add nodeval=%d carryin=%d,",val, carryin);
        newnode->val=val1+val2+carryin-10;
        carryout=1;
    }
    if(curr==NULL)
    {
        head=newnode;
    }
    else
    {
        while(curr->next!=NULL)
        {
            curr=curr->next;
        }
        curr->next=newnode;
    }
    //printf(" in addnode currl1->val=%d carryout=%d\n", newnode->val,carryout);
    return carryout;
}

struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2)
{
    struct ListNode* currl1=l1;
    struct ListNode* currl2=l2;
    int carryin=0;
    int carryout;
    int l2val=0;
    int l1val=0;
    while(currl1!=NULL|| currl2!=NULL||carryin!=0)
    {
        l1val=(currl1!=NULL)?currl1->val:0;
        l2val=(currl2!=NULL)?currl2->val:0;
        currl1=currl1->next;
        currl2=currl2->next;
        carryout=addNode(l1val,l2val,carryin);
        carryin=carryout;
    }
    return head;
}
```
這題要考慮 

1.有進位的問題 
2.list 長短不一致的問題

這題還有小bug : double free or corruption (out): 0x0000000001fd0300 ***

不知道為什麼會一直有double free問題
test case:
[0]
[0]



原本addTwoNumbers是寫成 下面兩種

但其實這兩種 寫法很直覺 但 if-else 巢狀迴圈會太複雜  


尤其第一種會有bug (一度卡很久)

```c
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2)
{
	struct ListNode* currl1=l1;
	struct ListNode* currl2=l2;
	int carryin=0;
	int carryout;
	while(currl1!=NULL|| currl2!=NULL||carryin!=0){
		if(currl1==NULL && currl2!=NULL){
			...
		}
		if(currl2==NULL&& currl1!=NULL){
			...
		}
		if(currl1!=NULL&& currl2!=NULL){
			... //move currl1 and currl2 points to the next one
		}

		if(currl1==NULL&& currl2==NULL){
			... //now both curr1 and curr2 are null,
				//the program runs into a bug without reset carryin
		}
		carryin=carryout;
	}
	return head;
}
```

```c

struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2)
{
	struct ListNode* currl1=l1;
	struct ListNode* currl2=l2;
	int carryin=0;
	int carryout;
	while(currl1!=NULL|| currl2!=NULL||carryin!=0){
		if(currl1==NULL && currl2!=NULL){
			...
		}
		else{
			if(currl2==NULL&& currl1!=NULL){
				...
			}
			else{
				if(currl1!=NULL&& currl2!=NULL){
					...
				}
				else{
					if(currl1==NULL&& currl2==NULL){
						...
					}
				}
			}
		}
		carryin=carryout;
	}
	return head;
}
```

