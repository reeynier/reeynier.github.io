---
layout: post
title:  "Reverse Nodes in k-Group Problem"
categories: [ Data Structure ]
tags: [ Linked List, Recursion, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 25. Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.
---

<br />

## Description

LeetCode Problem 25. 

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

 

Example 1:
```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

Example 2:
```
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

Example 3:
```
Input: head = [1,2,3,4,5], k = 1
Output: [1,2,3,4,5]
```

Example 4:
```
Input: head = [1], k = 1
Output: [1]
```
 

Constraints:

* The number of nodes in the list is in the range sz.
* 1 <= sz <= 5000
* 0 <= Node.val <= 1000
* 1 <= k <= sz


<br />

## Sample C++ Code


```c
class Solution {
public:
int length(ListNode * node){
    int count=0;
    while(node){
        count++;
        node=node->next;
    }
    return count;
}
ListNode* reverseKGroup(ListNode* head, int k) {
   if (length(head) < k)return head;
   ListNode * cur=head;
   ListNode * prev=NULL, *next=NULL;
   while (int i=0; i < k; i++){
       next=cur->next;
       cur->next=prev;
       prev=cur;
       cur=next;
   }
   head->next=reverseKGroup(cur, k);
   return prev;
 }
};
```
