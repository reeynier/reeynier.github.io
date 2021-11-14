---
layout: post
title:  "Remove Duplicates from Sorted List II Problem"
categories: [ Data Structure ]
tags: [ Linked List, Two Pointers, Leetcode ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 82. Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.
---

<br />

## Description

LeetCode Problem 82. 

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

 

Example 1:
```
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

Example 2:
```
Input: head = [1,1,1,2,3]
Output: [2,3]
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
        if ((head == NULL) || (head->next == NULL))
            return head;
        
        ListNode* curr = head;
        map<int, int> cnt;
        while (curr != NULL) {
            if (cnt.find(curr->val) != cnt.end()) {
                cnt[curr->val] ++;
            } else {
                cnt[curr->val] = 1;
            }
            curr = curr->next;
        }

        int first_num;
        bool is_empty = true;
        for (map<int,int>::iterator mit = cnt.begin(); mit != cnt.end(); 
            mit ++) {
            if (mit->second == 1) {
                first_num = mit->first;
                is_empty = false;
                break;
            }
        }
        if (is_empty)
            return NULL;
        
        curr = head;
        ListNode* new_head;
        ListNode* prev;
        while (curr != NULL) {
            if (curr->val == first_num) {
                new_head = curr;
                break;
            }
            curr = curr->next;
        }

        prev = new_head;
        curr = new_head->next;
        while (curr != NULL) {
            if (cnt[curr->val] == 1) {
                prev->next = curr;
                prev = prev->next;
            }
            curr = curr->next;
        }
        prev->next = NULL;
        return new_head;
    }
};
```
