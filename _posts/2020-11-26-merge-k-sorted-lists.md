---
layout: post
title:  "Merge K Sorted Lists Problem"
categories: [ Data Structure ]
tags: [ Linked List, Priority Queue, Leetcode ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: You are given an array of **k** linked-lists **lists**, each linked-list is sorted in ascending order.
---

<br />

## Description

You are given an array of **k** linked-lists **lists**, each linked-list is sorted in ascending order. Merge all the linked-list into one sorted linked-list and return it.


Example: 
```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

<br />

## Solution

This problem is similar to the [`merge two sorted lists problem`]({% post_url 2020-11-25-merge-two-sorted-lists %}).

We can compare the **k** heads of every linked list and get the node with the smallest value. We repeat this step until all lists are merged. The time complexity of this approach is O(kN), where N is the total number of nodes in all lists and k is the number of lists. This is because for every node in the merged list, it takes O(k) for comparison.

We can optimize this approach with a priority queue. We can insert all nodes into a priority queue. Then we create a new linked list by popping a node from the priority queue one at a time. As the priority queue will sort the nodes inserted into the queue, the final list popped will also be sorted.


The time complexity of this optimized approach is O(Nlogk). This is because the comparison cost will be reduced to O(logk) for every pop and insertion to priority queue.


<br />

## Sample C++ Code

This is a C++ implementation of the priority queue approach.

```c
#include <iostream>
#include <algorithm>
#include <vector>
#include <queue>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

ListNode* mergeKLists(vector<ListNode*>& lists) {
    priority_queue<int, vector<int>, greater<int>> pq;
    for (auto x : lists) {
        while (x != NULL) {
            pq.push(x->val);
            x = x->next;
        }
    }
    
    ListNode *temp = new ListNode();
    ListNode *head = temp;
    while (!pq.empty()) {
        temp->next = new ListNode(pq.top());
        pq.pop();
        temp = temp->next;
    }
    return head->next;
}

int main() {
    vector<ListNode*> lists;

    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(4);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(1);
    l2->next = new ListNode(3);
    l2->next->next = new ListNode(4);

    ListNode* l3 = new ListNode(2);
    l3->next = new ListNode(6);

    lists.push_back(l1);
    lists.push_back(l2);
    lists.push_back(l3);

    ListNode* head = mergeKLists(lists);
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    return 0;
}
```
