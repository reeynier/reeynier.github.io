---
layout: post
title:  "Reverse Linked List Problem"
categories: [ Algorithm ]
tags: [ Linked List, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
---

<br />

## Description

Reverse a singly linked list.


Example: 
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

<br />

## Solution

To reverse the linked list, we need to modify the next pointer in each node to point to the previous node in the list. Let us consider an example:
```
1 -> 2 -> 3
```

If we would like to reverse this list, we need to point node 2 to node 1, and then point node 3 to node 2. To do that, we first use a pointer *nextNode* to record the next node of node 2 (*currNode*), which is node 3. And we use a pointer *prevNode* to point to the previous node of node 2, which is node 1.
```
prevNode      currNode      nextNode
   1      ->     2      ->     3      ->    NULL
```
Then we point *currNode's* next pointer to the *prevNode*.
```
prevNode      currNode      nextNode
   1      <-     2      ->     3      ->    NULL
```
Then we move all three pointers to handle node 3.
```
              prevNode      currNode      nextNode
   1      <-     2      ->     3      ->    NULL
```
Again, we point *currNode's* next pointer to the *prevNode*.
```
              prevNode      currNode      nextNode
   1      <-     2      <-     3      ->    NULL
```
Then we move all three pointers again, and repeat the above steps until *currNode* is NULL. This means we reach the end of the list.
```
                            prevNode      currNode      nextNode
   1      <-     2      <-     3      ->    NULL
```
Now we finish reversing the linked list. We can return *prevNode*, which is the head node of the reversed list.

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

ListNode* reverseList(ListNode* head) {
    ListNode* prevNode;
    ListNode* nextNode;
    ListNode* currNode;
    
    if ((head == NULL) || (head->next == NULL))
        return head;
    
    currNode = head->next;
    prevNode = head;
    head->next = NULL;
    
    while (currNode != NULL) {
        nextNode = currNode->next;
        currNode->next = prevNode;
        prevNode = currNode;
        currNode = nextNode;
    }
    
    return prevNode;   
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

    ListNode* head = reverseList(lhead);
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    return 0;
}
```
