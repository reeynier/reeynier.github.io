---
layout: post
title: "Linked List Random Node Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Linked List, Math, Reservoir Sampling, Randomized ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 382. Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

---

<br />

## Description

LeetCode Problem 382.

Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

Implement the Solution class:
* Solution(ListNode head) Initializes the object with the integer array nums.
* int getRandom() Chooses a node randomly from the list and returns its value. All the nodes of the list should be equally likely to be choosen.

Example 1:
```
Input
["Solution", "getRandom", "getRandom", "getRandom", "getRandom", "getRandom"]
[[[1, 2, 3]], [], [], [], [], []]
Output
[null, 1, 3, 2, 2, 3]
Explanation
Solution solution = new Solution([1, 2, 3]);
solution.getRandom(); // return 1
solution.getRandom(); // return 3
solution.getRandom(); // return 2
solution.getRandom(); // return 2
solution.getRandom(); // return 3
// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
```

Constraints:
* The number of nodes in the linked list will be in the range [1, 10^4].
* -10^4 <= Node.val <= 10^4
* At most 10^4 calls will be made to getRandom.

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
    ListNode* HeadNode;
    Solution(ListNode* head) {
       HeadNode = head;
    }
    int getRandom() {
        int res, len = 1;
        ListNode* x = HeadNode;
        while(x){
            if(rand() % len == 0){
                res = x->val;
            }
            len++;
            x = x->next;
        }
        return res;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(head);
 * int param_1 = obj->getRandom();
 */
```


