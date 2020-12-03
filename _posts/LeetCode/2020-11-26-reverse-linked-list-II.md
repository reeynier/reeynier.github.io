---
layout: post
title:  "Reverse Linked List II Problem"
categories: [ Data Structure ]
tags: [ Linked List, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 92. Reverse a linked list from position m to n. 
---

<br />

## Description

LeetCode Problem 92. Reverse a linked list from position **m** to **n**. Do it in one-pass. Note: 1 ≤ m ≤ n ≤ length of list.

Example: 
```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

<br />

## Solution

This problem is similar to the [`reverse linked list problem`]({% post_url LeetCode/2020-11-26-reverse-linked-list %}). The difference is we only need to reverse the nodes from position *m* to *n*. 

We can iterate through the list. When we reach the *m-1*th node, we use a pointer (*head_r*) to record this node. This pointer will point to the head node of the reversed sub list, or will be the head node of the reversed sub list (for the m = 1 case).

When we reach the *m*th node, we also use a pointer (*tail_r*) to record this node. This will be the tail node of the reversed sub list. We also start reversing the list from this node. We can use the same method in the [`reverse linked list problem`]({% post_url LeetCode/2020-11-26-reverse-linked-list %}).

When we reach the *n*th node, we finish reversing the list. We then point the *tail_r* pointer to the *n+1*th node, and point the *head_r* pointer to the *n*th node. In this way, we can reverse the sub list in place. 

We also need to handle the case (m = 1) carefully. In this case, we set *head_r* node to be the *n*th node, and return *head_r* node as the head node of the new list.

The time complexity of the approach is O(n), and the space complexity is O(1).

<br />

## Sample C++ Code

This is a C++ implementation of the above approach.

```c
#include <iostream>
#include <algorithm>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

ListNode* reverseBetween(ListNode* head, int m, int n) {
    if ((head == NULL) || (head->next == NULL))
        return head;
    if (m == n)
        return head;
    
    int i = 1;
    ListNode* curr = head;
    ListNode* prev = NULL;
    ListNode* tmp;
    ListNode* tail_r;
    ListNode* head_r = NULL;
    while (curr != NULL) {
        if ((i >= m) && (i <= n)) {
            if (i == m) {
                tail_r = curr;
            }
            if (i == n) {
                tail_r->next = curr->next; 
                if (head_r == NULL) {
                    head_r = curr;
                } else {
                    head_r->next = curr;
                }
            }
            tmp = curr;
            curr = curr->next;
            tmp->next = prev;
            prev = tmp;
            i ++;
        } else {
            if (i == m - 1)
                head_r = curr;
            i ++;
            prev = curr;
            curr = curr->next;
        }
    }
    if (m == 1)
        return head_r;
    else
        return head;
}

int main() {
    ListNode* lhead = new ListNode(1);
    ListNode* curr = lhead;
    curr->next = new ListNode(2);
    curr = curr->next;
    curr->next = new ListNode(3);
    curr = curr->next;
    curr->next = new ListNode(4);
    curr = curr->next;
    curr->next = new ListNode(5);

    int m = 2, n = 4;

    ListNode* head = reverseBetween(lhead, m, n);
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    return 0;
}
```
