---
layout: post
title: "Linked List Cycle II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Linked List, Two Pointers ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 142. Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

---

<br />

## Description

LeetCode Problem 142.

Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. 

Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.

Example 1: 
```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

Example 2: 
```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

Example 3: 
```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

Constraints:
* The number of the nodes in the list is in the range [0, 10^4].
* -10^5 <= Node.val <= 10^5
* pos is -1 or a valid index in the linked-list.

<br />

## Sample C++ Code


```c
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if ((head == NULL) || (head->next == NULL))
            return NULL;
        
        ListNode *p1 = head->next;
        ListNode *p2 = head->next->next;
        
        while ((p1 != p2) && (p2 != NULL) && (p2->next != NULL)) {
            p1 = p1->next;
            p2 = p2->next->next;
        }
        if ((p2 == NULL) || (p2->next == NULL))
            return NULL;
        
        p1 = head;
        while (p1 != p2) {
            p1 = p1->next;
            p2 = p2->next;
        }
        return p1;
    }
};
```


