---
layout: post
title:  "Partition List Problem"
categories: [ Algorithm ]
tags: [ Linked List, Two Pointers, Leetcode ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 86. Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.
---

<br />

## Description

LeetCode Problem 86. 

Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

 

Example 1:
```
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

Example 2:
```
Input: head = [2,1], x = 2
Output: [1,2]
```

Constraints:

* The number of nodes in the list is in the range [0, 200].
* -100 <= Node.val <= 100
* -200 <= x <= 200

<br />

## Sample C++ Code


```c
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        if (head == NULL)
            return NULL;
        ListNode* head_l = NULL;
        ListNode* head_ge = NULL;
        ListNode* curr_l;
        ListNode* curr_ge;
        
        ListNode* curr = head;
        while (curr != NULL) {
            if (curr->val < x) {
                if (head_l == NULL) {
                    head_l = curr;
                    curr_l = curr;
                } else {
                    curr_l->next = curr;
                    curr_l = curr_l->next;
                }
            } else {
                if (head_ge == NULL) {
                    head_ge = curr;
                    curr_ge = curr;
                } else {
                    curr_ge->next = curr;
                    curr_ge = curr_ge->next;
                }
            }
            curr = curr->next;
        }

        if (head_l == NULL) {
            curr_ge->next = NULL;
            return head_ge;
        } else if (head_ge == NULL) {
            curr_l->next = NULL;
            return head_l;
        }
        else {
            curr_l->next = head_ge;
            curr_ge->next = NULL;
            return head_l;
        }
        
    }
};
```
