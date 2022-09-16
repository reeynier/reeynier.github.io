---
layout: post
title: "Odd Even Linked List Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Linked List ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 328. Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

---

<br />

## Description

LeetCode Problem 328.

Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The first node is considered odd, and the second node is even, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problemin O(1)extra space complexity and O(n) time complexity.

Example 1:
```
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]
```

Example 2:
```
Input: head = [2,1,3,5,6,4,7]
Output: [2,3,6,7,1,5,4]
```

Constraints:
* n ==number of nodes in the linked list
* 0 <= n <= 10^4
* -10^6 <= Node.val <= 10^6

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
    ListNode* oddEvenList(ListNode* head) {
        ListNode* odd_t;
        ListNode* even_h;
        ListNode* even_t;
        
        if ((head == NULL) || (head->next == NULL))
            return head;
        
        int i = 1;
        odd_t = head;
        even_h = head->next;
        even_t = head->next;
        
        while (even_t != NULL) {
            if (even_t->next == NULL)
                break;
            odd_t->next = even_t->next;
            even_t->next = even_t->next->next;
            odd_t = odd_t->next;
            odd_t->next = even_h;
            even_t = even_t->next;
            
        }
        return head;
    }
};
```


