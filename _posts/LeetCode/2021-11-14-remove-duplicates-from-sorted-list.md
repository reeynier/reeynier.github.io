---
layout: post
title:  "Remove Duplicates from Sorted List Problem"
categories: [ Data Structure ]
tags: [ Linked List, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 83. Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.
---

<br />

## Description

LeetCode Problem 83. 

Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

 

Example 1:
```
Input: head = [1,1,2]
Output: [1,2]
```

Example 2:
```
Input: head = [1,1,2,3,3]
Output: [1,2,3]
```

Constraints:

* The number of nodes in the list is in the range [0, 300].
* -100 <= Node.val <= 100
* The list is guaranteed to be sorted in ascending order.

<br />

## Sample C++ Code


```c
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* currNode;
        ListNode* prevNode;
        
        if ((head == NULL) || (head->next == NULL))
            return head;
        prevNode = head;
        currNode = head->next;
        
        while (currNode != NULL) {
            if (prevNode->val == currNode->val) {
                currNode = currNode->next;
                prevNode->next = currNode;
            } else {
                currNode = currNode->next;
                prevNode = prevNode->next;
            }
        }
        
        return head;
    }
};
```
