---
layout: post
title:  "Remove Nth Node From End of List Problem"
categories: [ Data Structure ]
tags: [ Linked List, Two Pointers, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 19. Given the head of a linked list, remove the nth node from the end of the list and return its head.
---

<br />

## Description

LeetCode Problem 19. 

Given the head of a linked list, remove the nth node from the end of the list and return its head.

 

Example 1:
```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

Example 2:
```
Input: head = [1], n = 1
Output: []
```

Example 3:
```
Input: head = [1,2], n = 1
Output: [1]
```

Constraints:

The number of nodes in the list is sz.
* 1 <= sz <= 30
* 0 <= Node.val <= 100
* 1 <= n <= sz

<br />

## Sample C++ Code


```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (head == NULL) 
            return NULL;
        ListNode* first = head;
        ListNode* second = new ListNode;
        second->next = head;
        
        int i = 1;
        while (first != NULL) {
            if (i > n) {
                second = second->next;
            }
            first = first->next;
            i ++;
        }
        if (second->next == head)
            head = head->next;
        else if (n > 1)
            second->next = second->next->next;
        else 
            second->next = NULL;
        return head;
        
    }
};
```
