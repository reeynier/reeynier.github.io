---
layout: post
title:  "Merge Two Sorted List Problem"
categories: [ Algorithm ]
tags: [ Linked List, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
---

<br />

## Description

Merge two sorted linked lists and return it as a new **sorted** list. The new list should be made by splicing together the nodes of the first two lists.


Example: 
```
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,5]

Input: l1 = [], l2 = []
Output: []
```

<br />

## Solution

The solution to this problem is straightforward. The idea is to compare the nodes from the two lists, and add the smaller node to the new list each time.

First, we set up a *head* list node to allow us to easily return the head of the merged list later. We also use three pointers *currNode*, *currNode1*, and *currNode2* to keep track of the current node in the merged list, list 1, and list 2, respectively. 

Then we do the following steps until either list 1 or list 2 is empty. If the value of *currNode1* is less than or equal to *currNode2*, we point *currNode's* next pointer to *currNode1*, and point *currNode1* to its next node. If the value of *currNode2* is less than *currNode1*, we point *currNode's* next pointer to *currNode2*, and point *currNode2* to its next node.

After these steps, at most one of list 1 and list 2 is non-empty. We can point *currNode* to the non-empty list's rest elements and return the *head* node.

The time complexity is O(n+m), where n and m are the length of the lists. The space complexity is O(1).


<br />

## Sample C++ Code

This is a C++ implementation of the binary search approach.

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

ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (l1 == NULL)
        return l2;
    if (l2 == NULL)
        return l1;

    ListNode* currNode1 = l1;
    ListNode* currNode2 = l2;
    ListNode* currNode;
    ListNode* head;
    
    currNode1 = l1;
    currNode2 = l2;
    
    if (l1->val <= l2->val) {
        head = l1;
        currNode = l1;
        currNode1 = currNode1->next;
    }
    else {
        head = l2;
        currNode = l2;
        currNode2 = currNode2->next;
    }
    
    while ((currNode1 != NULL) && (currNode2 != NULL)) {
        if (currNode1->val <= currNode2->val) {
            currNode->next = currNode1;
            currNode1 = currNode1->next;
            currNode = currNode->next;
        } else {
            currNode->next = currNode2;
            currNode2 = currNode2->next;
            currNode = currNode->next;
        }
    }
    if (currNode1 == NULL) {
        currNode->next = currNode2;
    } else {
        currNode->next = currNode1;
    }
    
    return head;
    
}

int main() {
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(2);
    l1->next->next = new ListNode(4);

    ListNode* l2 = new ListNode(1);
    l2->next = new ListNode(3);
    l2->next->next = new ListNode(4);

    ListNode* head = mergeTwoLists(l1, l2);
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    return 0;
}
```
