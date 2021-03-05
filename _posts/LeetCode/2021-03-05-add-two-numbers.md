---
layout: post
title:  "Add Two Numbers Problem"
categories: [ Data Structure ]
tags: [ Linked List, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 2. You are given two non-empty linked lists representing two non-negative integers.
---

<br />

## Description

LeetCode Problem 2. 

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 

Example 1:
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

Example 2:
```
Input: l1 = [0], l2 = [0]
Output: [0]
```

Example 3:
```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

Constraints:

* The number of nodes in each linked list is in the range [1, 100].
* 0 <= Node.val <= 9
* It is guaranteed that the list represents a number that does not have leading zeros.

<br />

## Sample C++ Code


This is a C++ solution using a `hash table`.

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        //result
        ListNode *res = new ListNode();
        ListNode *head = res;
        int carryOver = 0;
        int val1 = 0; 
        int val2 = 0; 
        
       while((l1 != NULL) || (l2 != NULL)) {
            if((l1 != NULL) && (l2 != NULL)) {
                //we have both values
                val1 = l1->val;
                val2 = l2->val; 
                //increment both
                l1 = l1->next;
                l2 = l2->next;
            }
            else if((l1 != NULL) && (l2 == NULL)) {
                //we have one value
                val1 = l1->val;
                val2 = 0;
                //increment l1
                l1 = l1->next;
            }
            else if((l1 == NULL) && (l2 != NULL)) {
                //we have one value
                val1 = 0;
                val2 = l2->val;
                //increment l2
                l2 = l2->next;
            }
           
           //add to result. 
           int sum = val1 + val2 + carryOver;
           res->val = sum % 10;
           carryOver = sum / 10;
           
           if(l1 != NULL || l2 != NULL || carryOver > 0) {
                ListNode* nextNode = new ListNode();
                res->next = nextNode;
                res = res->next;
           }
       }
        
       if(carryOver > 0)
           res->val = carryOver;
        
       return head;  
    }
};
```
