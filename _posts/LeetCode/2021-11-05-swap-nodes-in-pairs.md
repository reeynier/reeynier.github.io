---
layout: post
title:  "Swap Nodes in Pairs Problem"
categories: [ Data Structure ]
tags: [ Linked List, Recursion, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 24. Given a linked list, swap every two adjacent nodes and return its head.
---

<br />

## Description

LeetCode Problem 24. 

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

 

Example 1:
```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

Example 2:
```
Input: head = []
Output: []
```

Example 3:
```
Input: head = [1]
Output: [1]
```
 

Constraints:

* The number of nodes in the list is in the range [0, 100].
* 0 <= Node.val <= 100


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
    ListNode* swapPairs(ListNode* head) {
        if ((head == NULL) || (head->next == NULL))
            return head;
        ListNode* odd = head;
        ListNode* even = head->next;
        head = head->next;
        ListNode* tmp;
        
        while (even->next != NULL) {
            tmp = even->next;
            even->next = odd;
            if (tmp->next != NULL) {
                odd->next = tmp->next;
                odd = tmp;
                even = tmp->next;
            } else {
                odd->next = tmp;
                break;
            }
        }
        if (even->next == NULL) {
            even->next = odd;
            odd->next = NULL;
        }
        
        return head;
    }
};
```
