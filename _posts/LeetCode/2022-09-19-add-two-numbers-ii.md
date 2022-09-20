---
layout: post
title: "Add Two Numbers II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Linked List, Math, Stack ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 445. You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

---

<br />

## Description

LeetCode Problem 445.

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example 1: 
```
Input: l1 = [7,2,4,3], l2 = [5,6,4]
Output: [7,8,0,7]
```

Example 2:
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [8,0,7]
```

Example 3:
```
Input: l1 = [0], l2 = [0]
Output: [0]
```

Constraints:
* The number of nodes in each linked list is in the range [1, 100].
* 0 <= Node.val <= 9
* It is guaranteed that the list represents a number that does not have leading zeros.

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
    ListNode* addTwoNumbers(ListNode* h1, ListNode* h2) {
        stack<int> s1, s2;
        while (h1) {
            s1.push(h1->val);
            h1 = h1->next;
        }
        while (h2) {
            s2.push(h2->val);
            h2 = h2->next;
        }
        int carry_on = 0;
        ListNode *curr = NULL, *prev = NULL;
        while (s1.size() || s2.size() || carry_on) {
            int sum = carry_on;
            if (s1.size()) {
                sum += s1.top();
                s1.pop();
            }
            if (s2.size()) {
                sum += s2.top();
                s2.pop();
            }
            carry_on = sum / 10;
            prev = new ListNode(sum % 10);
            prev->next = curr;
            curr = prev;
        }
        return curr;
    }
};
```


