---
layout: post
title: "Linked List Cycle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Linked List, Two Pointers ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 141. Given head, the head of a linked list, determine if the linked list has a cycle in it.

---

<br />

## Description

LeetCode Problem 141.

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following thenextpointer. 

Internally, posis used to denote the index of the node thattail'snextpointer is connected to.Note thatposis not passed as a parameter.

Returntrue if there is a cycle in the linked list. Otherwise, return false.

Example 1:
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

Example 2:
```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.
```

Example 3:
```
Input: head = [1], pos = -1
Output: false
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
    bool hasCycle(ListNode *head) {
        if (head == NULL)
            return false;
        ListNode* firstNode = head->next;
        ListNode* secondNode = head;
        bool is_cycle = false;
        
        int cnt = 1;
        while ((firstNode != NULL) && (is_cycle == false)) {
            if (cnt % 2 == 0) {
                secondNode = secondNode->next;
            }
            firstNode = firstNode->next;
            cnt ++;
            if (firstNode == secondNode)
                is_cycle = true;
        }
        
        return is_cycle;
    }
};
```


