---
layout: post
title:  "Palindrome Linked List Problem"
categories: [ Data Structure ]
tags: [ Linked List, Two Pointer, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 234. Given a singly linked list, determine if it's a palindrome.
---

<br />

## Description

LeetCode Problem 234. Given a singly linked list, determine if it is a palindrome.


Example: 
```
Input: 1->2
Output: false

Input: 1->2->2->1
Output: true
```


<br />

## Solution

A simple solution is to iterate through the list, store the node values to an array and check whether the array is palindrome. The time complexity of this approach is O(n), and the space complexity is also O(n).

We can reduce the space complexity to O(1), without increasing the time complexity. This solution requires modifying the list. The solution is similar to the [`reverse linked list problem`]({% post_url LeetCode/2020-11-26-reverse-linked-list %}).


We first iterate through the list, and count the number of nodes in the list. 

Then we iterate through the list again. This time, if the current node is in the first half of the list, we reverse the list using the same approach as in the [`reverse linked list problem`]({% post_url LeetCode/2020-11-26-reverse-linked-list %}). We use a pointer *prev* to record the head of the reversed half of the list.

If the current node is in the second half of the list, we compare the current node with the prev node to check whether the list is palindrome. If the value of the prev node and the current node does not match, we return false. We repeat it until we reach the end of the list. Note that the prev node goes from the middle of the list to the beginning of the list, and the current node goes from the middle of the list to the end of the list. When we reach the end of the list and all node values match, we return true.

The time complexity of this approach is O(n), and the space complexity is O(1).

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

bool isPalindrome(ListNode* head) {
    ListNode* curr = head;
    ListNode* prev = head;
    ListNode* tmp;

    if ((head == NULL) || (head->next == NULL))
        return true;
    
    int cnt = 0;
    while (curr != NULL) {
        cnt ++;
        curr = curr->next;
    }

    curr = prev->next;
    int i = 1;
    prev->next = NULL;
    
    while (curr != NULL) {
        if ((cnt % 2 == 1) && (i == cnt / 2)) {
            curr = curr->next;
        } else if (i < cnt / 2) {
            tmp = curr;
            curr = curr->next;
            tmp->next = prev;
            prev = tmp;
        } else {
            if (curr->val != prev->val) {
                return false;
            } 
            curr = curr->next;
            prev = prev->next;
        }
        i ++;
    }
    return true;
}

int main() {
    ListNode* lhead = new ListNode(1);
    ListNode* curr = lhead;
    curr->next = new ListNode(2);
    curr = curr->next;
    curr->next = new ListNode(3);
    curr = curr->next;
    curr->next = new ListNode(2);
    curr = curr->next;
    curr->next = new ListNode(1);

    cout << isPalindrome(lhead) << endl;
    return 0;
}
```
