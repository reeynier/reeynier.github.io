---
layout: post
title: "Reorder List Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Linked List, Two Pointers, Stack, Recursion ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 143. You are given the head of a singly linked-list.  
---

<br />

## Description

LeetCode Problem 143.

You are given the head of a singly linked-list. The list can be represented as:
```
L_0 -> L_1 -> ... -> L_n - 1 -> L_n
```

Reorder the list to be on the following form:
```
L_0 -> L_n -> L_1 -> L_n - 1 -> L_2 -> L_n - 2 -> ...
```

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

Example 1: 
```
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```

Example 2: 
```
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```

Constraints:
* The number of nodes in the list is in the range [1, 5 * 10^4].
* 1 <= Node.val <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    void reorderList(ListNode* head) {
    	// Edge cases
        if ((!head) || (!head->next) || (!head->next->next)) return; 
        
        stack<ListNode*> my_stack;
        ListNode* ptr = head;
        int size = 0;
        while (ptr != NULL) {
        	// Put all nodes in stack
            my_stack.push(ptr);
            size++;
            ptr = ptr->next;
        }
        
        ListNode* pptr = head;
        for (int j=0; j<size/2; j++) {
        	// Between every two nodes insert the one in the top of the stack
            ListNode *element = my_stack.top();
            my_stack.pop();
            element->next = pptr->next;
            pptr->next = element;
            pptr = pptr->next->next;
        }
        pptr->next = NULL;
    }
};
```


