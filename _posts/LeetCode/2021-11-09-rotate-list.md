---
layout: post
title:  "Rotate List Problem"
categories: [ Data Structure ]
tags: [ Linked List, Two Pointers, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 61. Given the head of a linked list, rotate the list to the right by k places.
---

<br />

## Description

LeetCode Problem 61. 

Given the head of a linked list, rotate the list to the right by k places.

 

Example 1:
```
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```

Example 2:
```
Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

Constraints:

* The number of nodes in the list is in the range [0, 500].
* -100 <= Node.val <= 100
* 0 <= k <= 2 * 10^9



<br />

## Sample C++ Code


```c
ListNode* rotateRight(ListNode* head, int k) {
    if (!head || !head->next || k == 0) return head;
    ListNode *cur = head;
    int len = 1;
    while (cur->next && ++len) 
        cur = cur->next;
    cur->next = head;
    k = len - k % len;
    while (k--) 
        cur = cur->next;
    head = cur->next;
    cur->next = nullptr;
    return head; 
}
```
